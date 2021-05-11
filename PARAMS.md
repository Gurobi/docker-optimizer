
When using Gurobi, you can specify connection information by setting parameters 
in the API or by using a client license file. The full list of parameters can be found
in the [reference manual](https://www.gurobi.com/documentation/current/refman/parameters.html).
The following sections gives a quick guide to map license file to parameters.

# Connection to Gurobi Web License Service (WLS)

| Parameter	| License File |Purpose|
|-----------|--------------|-------|
|WLSAccessID | WLSACCESSID  | Access ID for Gurobi Web License Service (mandatory)
|WLSSecretKey| WLSSECRETKEY | Secret Key for Gurobi Web License Service (mandatory)
|LicenseID   | LICENSEID    | Type Integer, License ID for Gurobi Web License Service (mandatory)
|WLSTokenDuration   | WLSTOKENDURATION    | Token Duration

# Connection to Gurobi Cloud

| Parameter	| License File |Purpose|
|-----------|--------------|-------|
|[CloudAccessID](https://www.gurobi.com/documentation/current/refman/cloudaccessid.html)  | CLOUDACCESSID | Access ID for Gurobi Instant Cloud (mandatory)
|[CloudSecretKey](https://www.gurobi.com/documentation/current/refman/cloudsecretkey.html)| CLOUDSECRETKEY | Secret Key for Gurobi Instant Cloud (mandatory)
|[CloudPool](https://www.gurobi.com/documentation/current/refman/cloudpool.html)          | CLOUDPOOL | Cloud pool to use for Gurobi Instant Cloud instance|

# Connection to a self-managed cluster

| Parameter	| License File |Purpose|
|-----------|--------------|-------|
|[ComputeServer](https://www.gurobi.com/documentation/current/refman/computeserver.html)     | COMPUTESERVER |	Name of a node in the Remote Services cluster (mandatory)
|[ServerPassword](https://www.gurobi.com/documentation/current/refman/serverpassword.html)	 | PASSWORD | Client password for Remote Services cluster

# Connection to a self-managed cluster with a Router

| Parameter	| License File |Purpose|
|-----------|--------------|-------|
|[CSRouter](https://www.gurobi.com/documentation/current/refman/csrouter.html)	           | ROUTER | Router node for Remote Services cluster (mandatory)
|[ComputeServer](https://www.gurobi.com/documentation/current/refman/computeserver.html)   | COMPUTESERVER |	Name of a node in the Remote Services cluster (mandatory)
|[ServerPassword](https://www.gurobi.com/documentation/current/refman/serverpassword.html) | PASSWORD | Client password for Remote Services cluster

# Connection to a Cluster Manager

| Parameter	| License File |Purpose|
|-----------|--------------|-------|
|[CSManager](https://www.gurobi.com/documentation/current/refman/csmanager.html)         | CSMANAGER | URL for the Cluster Manager (mandatory)
|[CSAPIAccessID](https://www.gurobi.com/documentation/current/refman/csapiaccessid.html) | CSAPIACCESSID | Access ID for Gurobi Cluster Manager (mandatory)
|[CSAPISecret](https://www.gurobi.com/documentation/current/refman/csapisecret.html)	 | CSAPISECRET | Secret key for Gurobi Cluster Manager (mandatory)
|[CSBatchMode](https://www.gurobi.com/documentation/current/refman/csbatchmode.html)     | CSBATCHMODE | Controls Batch-Mode optimization

# Common parameters to Gurobi Cloud and Compute Server

| Parameter	| License File |Purpose|
|-----------|--------------|-------|
|[ServerTimeout](https://www.gurobi.com/documentation/current/refman/servertimeout.html)   | SERVERTIMEOUT | Network timeout interval
|[CSPriority](https://www.gurobi.com/documentation/current/refman/cspriority.html)	       | PRIORITY | Job priority for Remote Services job
|[CSQueueTimeout](https://www.gurobi.com/documentation/current/refman/csqueuetimeout.html) | QUEUETIMEOUT | Queue timeout for new jobs
|[CSGroup](https://www.gurobi.com/documentation/current/refman/csgroup.html)	           | GROUP | Group placement request for cluster
|[CSTLSInsecure](https://www.gurobi.com/documentation/current/refman/cstlsinsecure.html)   | CSTLSINSECURE | Use insecure mode in Transport Layer Security (TLS)
|[CSIdleTimeout](https://www.gurobi.com/documentation/current/refman/csidletimeout.html)  | IDLETIMEOUT | Idle time before Compute Server kills a job
|[CSAppName](https://www.gurobi.com/documentation/current/refman/csappname.html)           | CSAPPNAME | Application name of the batches or jobs
|[CSClientLog](https://www.gurobi.com/documentation/current/refman/csclientlog.html)       | - | Turns logging on or off

# Connection to a Gurobi Token Server

| Parameter	| License File |Purpose|
|-----------|--------------|-------|
|[TokenServer](https://www.gurobi.com/documentation/current/refman/tokenserver.html)	    | TOKENSERVER | Name of your token server (mandatory)
|[ServerPassword](https://www.gurobi.com/documentation/current/refman/serverpassword.html)	| PASSWORD | Client password for token server
|[TSPort](https://www.gurobi.com/documentation/current/refman/tsport.html)	                | PORT | Token server port number
|[ServerTimeout](https://www.gurobi.com/documentation/current/refman/servertimeout.html)    | SERVERTIMEOUT | Network timeout interval
