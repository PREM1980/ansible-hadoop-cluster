# Ansible Role: Setup a hadoop cluster

This scripts a multi node cluster for hadoop

## How to setup the hadoop cluster

1. Clone this repository
2. vagrant up

Once the cluster is up in running.
1. Login into node1 as hduser.
2. Source the ~/.bashrc to setup the env variables.
3. Set java_home in hadoop directory - /usr/local/hadoop/etc/hadoop/hadoop-env.sh (ansible tasks will be added)
4. Format node - /usr/local/hadoop/bin/hadoop namenode -format
5. Start hadoop	- /usr/local/hadoop/sbin/start-all.sh
6. Check services are running using jps command	jps
7. Check all node is running	sudo netstat -plten | grep java
8. Create a temp directory	mkdir -p /tmp/gutenberg(tasks already 
9. Copy the contents	http://www.gutenberg.org/cache/epub/20417/pg20417.txt
10. Create the hdfs directory	hdfs dfs -mkdir -p /user/hduser
11. Copy files /tmp to hdfs	hadoop hdfs -copyFromLocal /tmp/gutenberg /user/hduser/gutenberg
12. To run the example to to this folder - /usr/local/hadoop/share/hadoop/mapreduce	hadoop jar hadoop*examples*.jar wordcount /user/hduser/gutenberg /user/hduser/gutenberg-output
13. Copy the output - hadoop hdfs -getmerge /user/hduser/gutenberg-output /tmp/gutenberg-output


## License

MIT / BSD

