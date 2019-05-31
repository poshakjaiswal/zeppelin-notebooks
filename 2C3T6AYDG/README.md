## Do below steps to setup HortoniaBank tests for Ranger/Atlas :

##### Password less ssh across all nodes with gateway/ambari/appliance node (also needed password less ssh with self)

##### Add below components if not present : <br>
- Ranger 		`(Password to be set as Rangerpassword@123)`
- Atlas		`(Password to be set as admin123)`
- Hive
- HBase
- Kafka		`(One broker on the same node as appliance)`
- Zeppelin	`(On the same node as appliance)`

##### Setup a KDC server (with default REALM as EXAMPLE.COM) and Enable kerberos in the cluster and have a admin principal created :
`kadmin.local -q "addprinc -pw admin admin/admin"
Principal : 	admin/admin@EXAMPLE.COM
Password : 		admin`

##### Enable all the Ranger plugins. This step creates the policy repo for each component.
But before running the setup disable the plugin again (to avoid permission issue enforced by Ranger).

##### Populate secondary fs url in /grid/0/hadoopqe/conf/suite.conf and do not put a "/" at end of the URI
Format : 	[acronym]://[server]:[port]
E.g:
`[secondaryfs]
USE_SECONDARY_FS = True
SECONDARY_FS_URL = nfs://hdpserver:1228`

##### Data and Media files needed for the test are hosted in qe-repo bucket and referred again from above suite.conf file :
`[hortoniabank]
NOTEBOOK_MEDIA_URL = http://qe-repo.s3.amazonaws.com/partener-test-data/notebook-media.tgz
RANGER_ATLAS_DATA_URL = http://qe-repo.s3.amazonaws.com/partener-test-data/ranger-atlas-data-csv.tgz
HORTONIA_MUNICH_DATA_URL = http://qe-repo.s3.amazonaws.com/partener-test-data/HortoniaMunichSetup-data-csv.tgz`

##### To trigger the script SSH in to Ambari/appliance node as root and run below:
`cd /grid/0/tools/hortoniabank
chmod +x setup.sh
./setup.sh`

#### P.S. : Run setup.sh in nohup or in screen
