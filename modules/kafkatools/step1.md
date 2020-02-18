# Kafka Tools


## Kafkacat

https://medium.com/@frank.munz/kafkacat-on-amazonlinux-centos-d7ded88042e8

    sudo yum update -y
    sudo yum install git -y
    # make sure you have the necessary dev tools avail, 
    # or run the ff command:
    sudo yum group install “Development Tools” -y
    git clone https://github.com/edenhill/kafkacat.git
    cd kafkacat/
    ./bootstrap.sh
    ./kafkacat -h

