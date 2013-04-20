nagios-glusterfs
================

Nagios Module for GlusterFS (v3.3)

Usage
-----

# Using by NRPE
{

nagios@monitor:~/> ./check_nrpe -H 10.4.20.69 -c check_gluster
GLUSTER OK - Volume data is Stable
}

nrpe.cfg
--------
{

command[check_glusterfs]=/usr/lib64/nagios/plugins/check_glusterfs -n 2 -v data
}

/etc/sudoers.d/nagios
---------------------
{

nrpe ALL=NOPASSWD:/usr/sbin/gluster volume info data
nagios ALL=NOPASSWD:/usr/sbin/gluster volume info data
}


command.cfg
-----------

{

define command {

        command_name    check_nrpe
        command_line    $USER1$/check_nrpe -H $HOSTADDRESS$ -c $ARG1
}
}

nagios_service.cfg
------------------

{

define service {

        check_command                  check_nrpe!check_glusterfs
        host_name                      gluster01.example.com
        notification_period            24x7
        notification_interval          0
        use                            generic-service
        service_description            storage_check_glusterfs
}
}

Original From
-------------
http://www.johnbertrand.com/code/check_gluster_pl.html
