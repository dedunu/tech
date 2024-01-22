---
layout: post
title: "Terraform: How to run a command after an RDS creation?"
---

I wanted to know how to run a command after creating an RDS instance with Terraform. This was the answer I got from AWS. Even though, Terraform shouldn't be used like this. 

```terraform
resource "aws_db_instance" "mydb" {
  engine         = "mysql"
  engine_version = "5.6.40"
  instance_class = "db.t1.micro"
  name           = "initial_db"
  username       = "example"
  password       = "1234"
  allocated_storage = "20"
  publicly_accessible = "true"
}

output "username" {
    value = "${aws_db_instance.mydb.username}"
}

output "address" {
    value = "${aws_db_instance.mydb.address}"
}

resource "null_resource" "test" {
  depends_on = ["aws_db_instance.mydb"] #wait for the db to be ready
  provisioner "local-exec" {
    command = "mysql -u ${aws_db_instance.mydb.username} -p${aws_db_instance.mydb.password} -h ${aws_db_instance.mydb.address} -e \"CALL mysql.rds_set_configuration('binlog retention hours', 24);\" "
  }
}
```

### Gists

- <https://gist.github.com/dedunumax/932b707caa3a5a5a3736dcdce326e6c4>

### Tags

- rds
- Amazon
- terraform
