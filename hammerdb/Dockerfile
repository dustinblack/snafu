FROM centos/tools

# install requirements
RUN rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum install -y expect python-elasticsearch wget tcl unixODBC-devel unixODBC

# install packages required for ms-sql
RUN curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
RUN ACCEPT_EULA=Y yum -y install msodbcsql17
RUN ACCEPT_EULA=Y yum -y install msodbcsql
RUN yum remove -y unixODBC-utf16 unixODBC-utf16-devel && yum -y clean all
RUN yum clean all -y

# clone the snafu repo
#RUN git clone https://github.com/mkarg75/snafu.git
# Download and install the hammer suite

RUN wget 'https://downloads.sourceforge.net/project/hammerdb/HammerDB/HammerDB-3.2/HammerDB-3.2-Linux-x86-64-Install?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fhammerdb%2Ffiles%2FHammerDB%2FHammerDB-3.2%2FHammerDB-3.2-Linux-x86-64-Install%2Fdownload&ts=1564587940&use_mirror=autoselect' -O hammer_installer
RUN mkdir /hammer
RUN chmod 755 hammer_installer
RUN ./hammer_installer --prefix /hammer --mode silent

COPY hammerdb/uid_entrypoint /usr/local/bin/

RUN chmod g+w /etc/passwd
RUN chmod 755 /usr/local/bin/uid_entrypoint
RUN /usr/local/bin/uid_entrypoint
