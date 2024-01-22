---
layout: post
title: Hadoop MultipleInputs Example
---

Let's assume you are working for ABC Group. And they have ABC America airline,  ABM Mobile, ABC Money, ABC Hotel, etc. ABC this and that. So you got multiple data sources. They have different types/columns. So you can't run single Hadoop Job on all the data.

You got several data files from all these businesses.

```
ABC_America_Airline_Jan_2015.txt

Date		SSN	        From	        To		Amount($)
01/15/15	12345678	CO		TX		200		
01/16/15	23452345	NV		UT		150
01/16/15	34252454	CA		CO		200		
01/16/15	56785678	CA		TX		150
01/17/15	43545666	LA		UT		200		
01/17/15	67856783	TX		CO		150

ABC_Books_Jan_2015.txt

Date		SSN             Amount($)	BookName
01/04/15	43545666	200		Microsoft Visual Basic Step By Step		
01/08/15	34252454	150		Hadoop Definitive Guide
01/14/15	34252454	200		Master Puppet
01/15/15	56785678	325		Ubuntu for System Administrator
01/16/15	43545666	451		Java, How to Program 7e		
01/17/15	23452345	487		C in a Nutshell

ABC_Mobile_Jan_2015.txt

SSN             Date            Type            Amount($)
12345678	01/01/15	PREPAID		300
43545666	01/04/15	POSTPAID	234
34252454	01/14/15	PREPAID		300
56785678	01/17/15	PREPAID		234
23452345	01/30/15	PREPAID		300
67856783	01/31/15	POSTPAID	234
```

(Edited this data file 33 times to get it aligned. ;) Don't tell anyone!)

So your job is to calculate the total amount that one person spent for ABC group. For this, you can run jobs for each company and then run another job to calculate the sum. But what I'm going to tell you is "NOOOO! You can do this with one job." Your Hadoop administrator will love this idea.

You need to develop custom InputFormat and a custom RecordReader. I have created both of these classes inside the custom InputFormat class. Sample InputFormat should look like below.

```java
package org.dedunu.hadoop.muiltiinputsample;

import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.InputSplit;
import org.apache.hadoop.mapreduce.RecordReader;
import org.apache.hadoop.mapreduce.TaskAttemptContext;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.input.LineRecordReader;

import java.io.IOException;

/**
 * Created by dedunu on 5/21/15.
 */
public class AirlineInputFormat extends FileInputFormat<Text, Text> {
    public RecordReader<Text, Text> createRecordReader(InputSplit split, TaskAttemptContext context) throws IOException, InterruptedException {
        return new AirlineInputFormatClass();
    }

    public class AirlineInputFormatClass extends RecordReader<Text, Text> {
        private LineRecordReader lineRecordReader = null;
        private Text key = null;
        private Text value = null;

        @Override
        public void close() throws IOException {
            if (null != lineRecordReader) {
                lineRecordReader.close();
                lineRecordReader = null;
            }
            key = null;
            value = null;
        }

        @Override
        public Text getCurrentKey() throws IOException, InterruptedException {
            return key;
        }

        @Override
        public Text getCurrentValue() throws IOException, InterruptedException {
            return value;
        }

        @Override
        public float getProgress() throws IOException, InterruptedException {
            return lineRecordReader.getProgress();
        }

        @Override
        public void initialize(InputSplit split, TaskAttemptContext context) throws IOException, InterruptedException {
            close();

            lineRecordReader = new LineRecordReader();
            lineRecordReader.initialize(split, context);
        }

        @Override
        public boolean nextKeyValue() throws IOException, InterruptedException {
            if (!lineRecordReader.nextKeyValue()) {
                key = null;
                value = null;
                return false;
            }

            // This is where you should implement your custom logic.
            Text line = lineRecordReader.getCurrentValue();
            String str = line.toString();
            String[] arr = str.split("\\t");

            key = new Text(arr[1]);
            value = new Text(arr[4]);

            return true;
        }

    }
}
```

`nextKeyValue()` method is the place where you should code according to your data files.

Developing custom `InputFormat` classes is not just enough. Also, you need to change the `main` class in your job. Your `main` class should look like below.

```java
package org.dedunu.hadoop.muiltiinputsample;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.lib.input.MultipleInputs;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.mapreduce.lib.output.TextOutputFormat;

import java.io.IOException;

/**
 * Created by dedunu on 5/21/15.
 */
public class Main {
    public static void main(String[] args) throws IOException, ClassNotFoundException, InterruptedException {
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "ABC Sample Job");
        job.setJarByClass(Main.class);
        job.setReducerClass(SampleReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(Text.class);
        job.setOutputFormatClass(TextOutputFormat.class);

        MultipleInputs.addInputPath(job, new Path(args[0]), AirlineInputFormat.class, SampleMapper.class);
        MultipleInputs.addInputPath(job, new Path(args[1]), BookInputFormat.class, SampleMapper.class);
        MultipleInputs.addInputPath(job, new Path(args[2]), MobileInputFormat.class, SampleMapper.class);

        FileOutputFormat.setOutputPath(job, new Path(args[3]));

        boolean result = job.waitForCompletion(true);

        System.exit(result ? 0 : 1);
    }
}
```

Line no. `26-28` adds your custom inputs to the job. Also, you don't want to set the Mapper class separately because you can't set it too. If you want you can develop separate mapper classes for your different file types. I'll write a blog post about that method also.
To build the JAR from my sample project you need Maven. Run below command to build JAR from Maven project. You can find the JAR file inside the target folder once you build the project.

```console
$ mvn clean install
```

```
/
|----/user
     |----/hadoop
          |----/airline_data
          |    |----/airline.txt
          |----/book_data
          |    |----/book.txt
          |----/mobile_data
               |----/mobile.txt
```

With this change, you may have to change the way you run the job. My file structure looks like above. I have different folders for different types. You can run the job from the command below.

```console
$ hadoop jar /vagrant/muiltiinput-sample-1.0-SNAPSHOT.jar /user/hadoop/airline_data /user/hadoop/book_data /user/hadoop/mobile_data output_result
```

If you have followed all the steps properly you will get a job's output like this.

```console
15/05/21 09:48:09 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
15/05/21 09:48:10 WARN mapreduce.JobSubmitter: Hadoop command-line option parsing not performed. Implement the Tool interface and execute your application with ToolRunner to remedy this.
15/05/21 09:48:10 INFO input.FileInputFormat: Total input paths to process : 1
15/05/21 09:48:10 INFO input.FileInputFormat: Total input paths to process : 1
15/05/21 09:48:10 INFO input.FileInputFormat: Total input paths to process : 1
15/05/21 09:48:10 INFO mapreduce.JobSubmitter: number of splits:3
15/05/21 09:48:10 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1432197111554_0002
15/05/21 09:48:10 INFO impl.YarnClientImpl: Submitted application application_1432197111554_0002
15/05/21 09:48:10 INFO mapreduce.Job: The url to track the job: http://hdp101.local:8088/proxy/application_1432197111554_0002/
15/05/21 09:48:10 INFO mapreduce.Job: Running job: job_1432197111554_0002
15/05/21 09:48:17 INFO mapreduce.Job: Job job_1432197111554_0002 running in uber mode : false
15/05/21 09:48:17 INFO mapreduce.Job:  map 0% reduce 0%
15/05/21 09:48:26 INFO mapreduce.Job:  map 33% reduce 0%
15/05/21 09:48:27 INFO mapreduce.Job:  map 100% reduce 0%
15/05/21 09:48:32 INFO mapreduce.Job:  map 100% reduce 100%
15/05/21 09:48:33 INFO mapreduce.Job: Job job_1432197111554_0002 completed successfully
15/05/21 09:48:33 INFO mapreduce.Job: Counters: 49
	File System Counters
		FILE: Number of bytes read=276
		FILE: Number of bytes written=425877
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=1457
		HDFS: Number of bytes written=79
		HDFS: Number of read operations=12
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=2
	Job Counters 
		Launched map tasks=3
		Launched reduce tasks=1
		Data-local map tasks=3
		Total time spent by all maps in occupied slots (ms)=22080
		Total time spent by all reduces in occupied slots (ms)=3382
		Total time spent by all map tasks (ms)=22080
		Total time spent by all reduce tasks (ms)=3382
		Total vcore-seconds taken by all map tasks=22080
		Total vcore-seconds taken by all reduce tasks=3382
		Total megabyte-seconds taken by all map tasks=22609920
		Total megabyte-seconds taken by all reduce tasks=3463168
	Map-Reduce Framework
		Map input records=18
		Map output records=18
		Map output bytes=234
		Map output materialized bytes=288
		Input split bytes=825
		Combine input records=0
		Combine output records=0
		Reduce input groups=6
		Reduce shuffle bytes=288
		Reduce input records=18
		Reduce output records=6
		Spilled Records=36
		Shuffled Maps =3
		Failed Shuffles=0
		Merged Map outputs=3
		GC time elapsed (ms)=166
		CPU time spent (ms)=2100
		Physical memory (bytes) snapshot=987889664
		Virtual memory (bytes) snapshot=2790764544
		Total committed heap usage (bytes)=721813504
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters 
		Bytes Read=0
	File Output Format Counters 
		Bytes Written=79
```

The job will create a folder called output_result. If you want to see the content you can run below command.

```console
$ hdfs dfs -cat output_result1/part*
```

I ran my sample project on my sample data set. My result file looked like below.

```
12345678 500
23452345 937
34252454 850
43545666 1085
56785678 709
67856783 384
```

Source code of this project is available on [GitHub](https://github.com/dedunu/hadoop-multiinput-sample)

#### Gistss

- <https://gist.github.com/dedunumax/132f2751c794342de53a>
- <https://gist.github.com/dedunumax/96594b09d0f566e88ced>
- <https://gist.github.com/dedunumax/f55f928250b85f9fc801>
- <https://gist.github.com/dedunumax/8dbd361316c49fcb1fc2>

### Tags

- MultipleInputs
- custom RecordReader
- hadoop
- custom InputFormat