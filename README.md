
# Step-by-step TVK POC

## Requirements:

- One or more clusters running Kubernetes v1.17+
- CSI Driver with Snapshot enabled functionality (Hostpath option available, see step 3) 
- NFS or S3 bucket for storing your backups 

## Setup TrilioVault for Kubernetes

### 1. Install TVK

TVK install can be done through Helm or OCP Operator Hub.  Be sure to run the "Preflight Check" scripts before installing, as outlined in the documentation. 

TVK Install Documentation - https://docs.trilio.io/kubernetes/use-triliovault/installing-triliovault 

### 2. Get a license

Ask your Solutions Architect or Solutions Engineer for a TVK license for each cluster used for the POC. Additionally, you can get a Free Trial or Basic Edition license at: https://www.trilio.io/plans/

TVK Lincensing Documentation - https://docs.trilio.io/kubernetes/overview/licensing

### 3. Set up CSI Driver

TVK requires a CSI Driver with Snapshot enable capabilties. Ensure the proper CSI Driver is configured with your cluster or use a Hostpath CSI Driver as outlined in the TVK Documentation.  Ensure the Storage Class for your CSI is the only Storage Class set to "Default", otherwise proper provisioning may not occur.  

List of CSI Drivers - https://kubernetes-csi.github.io/docs/drivers.html 
- Locate your CSI driver and see "Snapshotting" under the "Other Features" column

HostPath CSI Driver for TrilioVault for Kubernetes Documentation - https://docs.trilio.io/kubernetes/appendix/csi-drivers/hostpath-for-tvk 

### 4. Access TVK UI

Set up the TVK UI with DNS or Non-DNS/Local Environments.  Through the TVK UI users can create Custom Resources (Targets, BackupPlans, etc), perform Backups and Restores, and monitor the success and logging of Backup and Restore summaries.  

Accessing the UI Documentation - https://docs.trilio.io/kubernetes/use-triliovault/user-interface/accessing-the-ui 

### 5. Access TVK in OCP UI

Access TVK through Openshift by navigating to Operators->Installed Operators-> Trilio

Here users can create Custom Resources (Targets, BackupPlans, etc.) and Perform Backup and Restores.  Monitoring of Backup and Restore summaries are limited in the OCP UI. 

### 6. Create a Target

Configure you NFS or S3 bucket as your Target for storing backups

Create a Target Documentation - https://docs.trilio.io/kubernetes/overview/getting-started#create-a-target 

Target Examples Documentation - https://docs.trilio.io/kubernetes/architecture/custom-resource-definitions-application-1/triliovault-crds#backup-target 

## Test Application-centric Backup and Recovery

It is recommend to first test the scenarios of your choosing in the CLI, then test using the TVK UI.  Testing in the CLI will provide technical insight into Custom Resource creation and Backup/Recovery performance.  Once complete, reproduce scenarios in the TVK UI for a simplified experience, enhanced with monitoring capabilties.  

### Three ways to Restore

Applications in each scenario can be retored to a **new namespace, different namespace, or different cluster**. Explore any or all restore options with the 4 testing scenarios listed below.  See example YAML files for each restore option in the link below. 

Restore CRD examples - https://docs.trilio.io/kubernetes/architecture/custom-resource-definitions-application-1/triliovault-crds#restore 

### Using the TVK UI

See all sub-sections of the Management Console documentation to learn how to navigate the TVK UI when performing actions for each testing scenario.

Management Console Documentation - https://docs.trilio.io/kubernetes/use-triliovault/user-interface 

### Scenario 1: Label based Backup and Recovery

Use an application of your choosing or use the MySQL sample application provided in this repo - k8s-demo-app.yaml 

YAML files for this scenario are already present in this repo:  
mysql-label-backupplan.yaml  
mysql-label-backup.yaml  
demo-restore.yaml  

Label Example Documentation - https://docs.trilio.io/kubernetes/overview/getting-started#label-example 

### Scenario 2: Helm based Backup and Recovery 

Use a Helm deployed application of your choosing or use a "cockroachdb" application provided in this repo - cockroachdb-values.yaml

Helm Example Documentation - https://docs.trilio.io/kubernetes/overview/getting-started#helm-example 

### Scenario 3: Operator based Backup and Recovery

Use an Operator deployed application of your choosing or install the demo-etcd-operator provided in the TVK documentation link below. 

Operator Example Documentation - https://docs.trilio.io/kubernetes/overview/getting-started#operator-example 

### Scenario 4: Namespace based Backup and Recovery

Use an application of your choosing or use the Wordpress application provided in the TVK documenation link below. 

Namespace Example Documentation - https://docs.trilio.io/kubernetes/overview/getting-started#namespace-example

## Conclusion

For any additional questions please contact your Trilio Solutions Architect, Solutions Engineer, or contact Trilio directly through https://www.trilio.io/contact-us/. 

Thank you! 

## Known Issues and Workarounds

### TVK UI Setup

When using OCP, TVK UI can NOT be set up using Networking->Routes.  This is due to Trilio's unique Ingress Controller and the architecture design of the OCP used Ingress Controller.  Instead please follow the TVK Documentation on "Accessing the UI" - https://docs.trilio.io/kubernetes/use-triliovault/user-interface/accessing-the-ui 

### TVK Lincense

Note, TVK lincenses are unique to each cluster, if testing wishes to be done on a new cluster, a new license must be generated.  Please contact your Solutions Architect or Solutions Engineer for a new license.  

