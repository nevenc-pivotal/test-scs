Test SCS Services: PART 1 - Testing Service Registry
----------------------------------------------------

In this short exercise, we will test Spring Cloud Services (SCS) Service Registry, with two sample applications
'greeter' and 'message-generation'. Both applications will get registered automatically with the instance of
service registry upon deployment. One application 'greeter' uses service registry to lookup the other application
'message-generation' and retrieve message to display.


Here are the steps to test your SCS Service Registry.

1a) Download git repo, https://github.com/nevenc-pivotal/scs-test

   git clone https://github.com/nevenc-pivotal/scs-test
   cd scs-test

1b) Alternatively, if you don't have git client on your (Windows) machine, you can always download the zip package, e.g.

   https://github.com/nevenc-pivotal/test-scs/archive/master.zip

   This will download test-scs-master.zip file to your Downloads folder. Please unpack the file and change directory
   to the unpacked folder.

2) Using your browser, login to your PCF Apps Manager as a standard user, e.g. https://login.system.YOURDOMAIN.COM

3) Go to your target ORG/Space, e.g. my-org/development

4a) Click on "Add Service" --> "Service Registry" --> "Select this plan"

   Instance Name: my-service-registry
   Add to Space:  development
   Bind to App:   [do not bind]

   --> Click "Add"

   New service registry (Eureka instance) is being created.

4b) Alternatively to step 4a) -  you can use CF CLI to create a service instance of Eureka (Service Registry), e.g.

     cf cs p-service-registry standard my-service-registry

5) Click on "Manage" under "my-service-registry" service, and within 1-2 minutes, you should see your new Eureka instance, e.g.

     https://eureka-3f067bca-34d4-4d42-9812-cce3a1e72b0b.system.YOURDOMAIN.COM/

   GREAT! Your service registry creation worked!

6) Now, let's deploy two applications that will automatically register with the service registry.

7) Edit manifest-test-eureka.yml file and update CF_TARGET with the API for your PCF, e.g.

     CF_TARGET: https://api.system.YOURDOMAIN.COM

8) Deploy two applications with cf push and given manifest, e.g.

     cf push -f manifest-test-eureka.yml

   Wait for the applications to deploy (2-4 minutes).

   Take a note of the 'greeting' application url, e.g.

     https://greeter-SOME_RANDOM_WORDS.apps.YOURDOMAIN.COM

9) Test the application, e.g.

   https://greeter-SOME_RANDOM_WORDS.apps.YOURDOMAIN.COM

   You should see the default greeting "Hello, Bob!".

9) Congratulations! Both your apps ('greeting' and 'message-generation') have registered with Eureka
   service registry. One app ('greeting') has successfully found the other app ('message-generation')
   and polled for the message to display.

10) You can find the apps registered in the Eureka service registry instance, e.g.

      https://eureka-3f067bca-34d4-4d42-9812-cce3a1e72b0b.system.YOURDOMAIN.COM/

    Look for "REGISTERED APPS" section.

11) Congratulations! Your Eureka (Service Registry) has been successfully configured.



