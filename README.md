# Hadoop-install

1. CentOs 에는 기본적으로 자바가 설치되어 있지 않지만, 다운로드 했던 자바를 지우거나 기존 자바를 삭제 할 경우 
   yum -y remove "java-*"
   

2. jdk 다운로드
   
    cd ~/Downloads

    (64비트인 경우)
    wget —no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz

    (32비트인 경우)
    wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jdk-8u60-linux-i586.tar.gz"


    cd ~/Downloads/
    tar –zxvf jdk-8u5-linux-x64.tar.gz
    mkdir /usr/java
    mv jdk1.8.0_05 /usr/java/jdk1.8

    vi /etc/profile

    밑에 export 3줄만 추가

    export JAVA_HOME=/usr/java/jdk1.8
    export PATH=$JAVA_HOME/bin:$PATH
    export CLASSPATH=$CLASSPATH:$JAVA_HOME/jre/lib/ext:$JAVA_HOME/lib/tools.jar

    # 실행
    source /etc/profile
    
    
    
    
    
    
    # SSH 설치 및 공개 키 설정 
    #   Hadoop클러스터에서 Master와 Slave들 간에 통신은 SSH를 이용함
    #   모든 컴퓨터에는  SSH가 설치되어 있어야 함
    #   Master에서 암호없이 Slave에 접속하기 위해서 공개 키가 필요함

    useradd hadoop
    su - hadoop
    ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
    cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
    chmod 0600 ~/.ssh/authorized_keys
    
    
    
3. 로컬호스트 접속했다가 나오기

    ssh localhost
    exit
    (ctrl + d)
    
    
4. 하둡 다운로드

    cd /home
    mkdir hadoop
    cd hadoop
    wget http://apache.tt.co.kr/hadoop/common/hadoop-2.7.1/hadoop-2.7.1.tar.gz
    tar -zxvf hadoop-2.7.1.tar.gz
    
    
5. 환경설정 

    $vi $HOME/.bashrc
    export JAVA_HOME=/usr/java/jdk1.8
    export HADOOP_CLASSPATH=${JAVA_HOME}/lib/tools.jar
    export HADOOP_HOME=/home/hadoop/hadoop-2.7.1
    export HADOOP_INSTALL=$HADOOP_HOME
    export HADOOP_MAPRED_HOME=$HADOOP_HOME
    export HADOOP_COMMON_HOME=$HADOOP_HOME
    export HADOOP_HDFS_HOME=$HADOOP_HOME
    export HADOOP_YARN_HOME=$HADOOP_HOME
    export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
    export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
    export JAVA_LIBRARY_PATH=$HADOOP_HOME/lib/native:$JAVA_LIBRARY_PATH

    $source $HOME/.bashrc
