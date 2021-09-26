如何在git上传新的工程

1.git init

2.git add .

3.git commit -m 'testname'

4.git remote add origin https://...

fatal: remote origin already exists，则执行以下语句：

​	$ git remote rm origin

5.git push origin master