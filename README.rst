DropletSync, Resource Cloning
##############################
:date: 2013-11-16
:tags: migrate, clone, sync, rackspace, aws, hpcloud, droplet
:category: \*nix
:version: 2.0.2-DO


The use cases
^^^^^^^^^^^^^

* Migrating from one provider to another
* Downgrading a droplet to a smaller size


What I have tested
^^^^^^^^^^^^^^^^^^

* Droplet to Droplet (Same OS)
* Droplet to Droplet (Similar OS i.e Ubuntu to Debian or Ubuntu 12.04 to 14.04)
* Droplet to Droplet (Different OSes i.e. Centos to Debian, see caveats)
* Other KVM VPS to Droplet (Some are better than others)
* Amazon EC2 to Droplet
* Rackspace cloud to Droplet
* Dedicated Server to Droplet


Caveats :
  There are two issues I have found while migrating droplets around. However, the most important caveat was related to the droplet type.  **You Must Have a Similar Droplet to Migrate Too**. 
  If you are using a multi-partition virtual machine to migrate to a droplet, you will have to manually migrate the partitions accordingly.  Which can be successfully accomplished by migrating to the droplet by hand. 
  Other than the one caveat, of having Similar Droplet, I have not had this process fail. It does sometimes get a little wonky when going between Different OSes (Centos to Debian, etc) and I do not suggest it in that case.

  
Testament that It Works :
  I know that this method works for a variety of situations, I have even had this process complete successfully when migrating to a droplet from **Amazon AMI Linux**. 

  
Available Options
^^^^^^^^^^^^^^^^^

All options can be set as exports in the environment which the script will use with attempting to perform the Sync Operation.


Enable More Verbosity in the script, Default is "False":
  VERBOSE="False or True"

Enable Debug Mode in the Script, Default is "False":
  DEBUG="False or True"

Add Additional Excludes to the script when Performing the Sync. This is a Space separated list, if you have files with spaces in the name you MUST escape them.
  USER_EXCLUDES=""

Change the Retry Max, Default is 5. This is useful on systems with High Load averages, which can cause the Sync Process to die.
  MAX_RETRIES="5"

Enable Inflammatory mode, Default is "False":
  INFLAMMATORY="False or True"
  
  
Estimated time of Completion
^^^^^^^^^^^^^^^^^^^^^^^^^^^^


**The Estimated time to completion based on Gigabytes of Consumed Space**
**Computations have been made using an average transfer rate of 20 Megabytes a second.**


============  ============
    The Estimated time
--------------------------
 Space Used     EST Time
============  ============
 10G          9    Minutes
 20G          17   Minutes
 40G          34   Minutes
 80G          68   Minutes
 160G         136  Minutes
 320G         272  Minutes
 620G         544  Minutes
 1200G        1088 Minutes
============  ============


Foot Notes
^^^^^^^^^^

When Performing a sync you should attempt to minimize load on your "Source" machine. The Sync script works great on a live system though if the load is too high it could cause the sync process to die.

When performing a sync on a system with a database, be aware that if you are writing a lot of data to the database you may want to shutdown the database engine while the sync is in process. By shutting down the database you can be sure that all of the data in the database was cloned without any sharding.
