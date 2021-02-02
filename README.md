nagios-glusterfs
================
Nagios Module for GlusterFS (v3.3)

*This plugin has been archived and no further development will be done.*

Usage
-----
    nagios@monitor:~/> /usr/lib64/nagios/plugins/check_nrpe -H 10.0.0.100 -c check_glusterfs
    GLUSTER OK - Volume data is Stable

    nagios@monitor:~/> /usr/lib64/nagios/plugins/check_nrpe -H 10.0.0.101 -c check_glusterfs
    GLUSTERFS CRITICAL - Brick count is 3, should be 4

nrpe.cfg
--------
    command[check_glusterfs]=/usr/lib64/nagios/plugins/check_glusterfs -n 2 -v data

/etc/sudoers.d/nagios
---------------------
    nrpe ALL=NOPASSWD:/usr/sbin/gluster volume info data
    nagios ALL=NOPASSWD:/usr/sbin/gluster volume info data


command.cfg
-----------
    define command {
        command_name    check_nrpe
        command_line    $USER1$/check_nrpe -H $HOSTADDRESS$ -c $ARG1
    }

nagios_service.cfg
------------------
    define service {
        check_command                  check_nrpe!check_glusterfs
        host_name                      gluster01.example.com
        notification_period            24x7
        notification_interval          0
        use                            generic-service
        service_description            storage_check_glusterfs
    }

Credits
-------
http://www.johnbertrand.com/code/check_gluster_pl.html
