# centos_lnmp

mkdir lnmp1.5

cd lnmp1.5

echo "FROM centos" >> Dockerfile

echo "RUN yum -y install wget && wget http://soft.vpser.net/lnmp/lnmp1.5beta.tar.gz -cO lnmp1.5beta.tar.gz && tar zxf lnmp1.5beta.tar.gz && cd lnmp1.5 && LNMP_Auto=\"y\" DBSelect=\"0\" PHPSelect=\"5\" SelectMalloc=\"1\" ./install.sh lnmp" >> Dockerfile

docker build - < Dockerfile

docker tag 37bea728bee2 he426100/lnmp:1.5
