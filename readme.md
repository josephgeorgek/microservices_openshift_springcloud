## Running Java Microservices on OpenShift using Source-2-Image 

Detailed description can be found here:

$ oc login -u system:admin
$ oc policy add-role-to-user cluster-reader system:serviceaccount:myproject:default

$ kubectl create clusterrolebinding admin --clusterrole=cluster-admin --serviceaccount=default:default

>oc login -u developer

projects and can switch between them with 'oc project <projectname>’:


employee

>oc new-app registry.access.redhat.com/redhat-openjdk-18/openjdk18-openshift~https://github.com/josephgeorgek/microservices_openshift_springcloud.git --name=employee --context-dir=employee-service

>oc set env bc/employee --from="secret/mongodb" --prefix=MONGO_

department

>oc new-app registry.access.redhat.com/redhat-openjdk-18/openjdk18-openshift~https://github.com/josephgeorgek/microservices_openshift_springcloud.git --name=department --context-dir=department-service -e EMPLOYEE_SERVICE=employee

>oc set env bc/department --from="secret/mongodb" --prefix=MONGO_

> oc start-build department

organization

>oc new-app registry.access.redhat.com/redhat-openjdk-18/openjdk18-openshift~https://github.com/josephgeorgek/microservices_openshift_springcloud.git --name=organization --context-dir=organization-service -e EMPLOYEE_SERVICE=employee -e DEPARTMENT_SERVICE=department


>oc set env bc/organization --from="secret/mongodb" --prefix=MONGO_




expose the service for external access

> oc expose svc employee

route.route.openshift.io/employee exposed
 
> oc expose svc department

route.route.openshift.io/department exposed
> oc expose svc organization
route.route.openshift.io/organization exposed