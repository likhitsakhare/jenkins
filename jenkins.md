// SONARQUBE INSTALLATION //

Install and configure Database

apt install openjdk-17-jdk -y
apt install postgresql -y
systemctl start postgresql
sudo -u postgres psql
>> CREATE USER linux PASSWORD 'redhat';
>> CREATE DATABASE sonarqube;
>> GRANT ALL PRIVILEGES ON DATABASE sonarqube TO linux;
>> \c sonarqube;
>> GRANT ALL PRIVILEGES ON SCHEMA public TO linux;
>> \q


Configure Linux Machine

sysctl -w vm.max_map_count=524288
sysctl -w fs.file-max=131072
ulimit -n 131072
ulimit -u 8192


Install and Configure Sonarqube

wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-25.5.0.107428.zip
apt install unzip -y
unzip sonarqube-25.5.0.107428.zip
mv sonarqube-25.5.0.107428 sonar
mv  sonar /opt/
cd /opt/sonar
vim conf/sonar.properties
>> sonar.jdbc.username=linux
>> sonar.jdbc.password=redhat
>> sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube

adduser sonar
chown sonar:sonar -R /opt/sonar
su sonar
cd /opt/sonar/bin/linux-x86-64
./sonar.sh start
./sonar.sh status

In SonarQube UI

Create your first project
Test it locally
Generate it's token and save it somewhere
It will give you some commands

In Jenkins UI

Install Plugins like SonarScanner and SonarQualityGate
Integrate SonarQube in System in Manage Jenkins with name and token generated in SonarQube
