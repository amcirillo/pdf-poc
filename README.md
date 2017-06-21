# rest-async-poc
**This is a POC project to illustrate how to build an asynchronous REST service in Camel**


This demo is intended to illustrate an asynchronous REST service that could be used to extend geography on an existing media plan. Since the operations required to do that will take some time we are designing this service to be asynchronous. The client will be given a UUID on the initial request that can then be used to check for completion status at a later point in time.

**Instructions for use:**

        1. This project will build a customized Fuse distribution. To build the distribution simply run "mvn clean install" in the top level folder
        
        2. After the build completes you will end up with a custom Fuse archive in distribution/karaf-assembly/async-poc-assembly-$VERSION.zip.
           Take this zip file and extract it somewhere. The start fuse by navigating into the distribution's bin folder and running the start script.

        3. Run a curl command to POST data to the addgeo endpoint
            curl -X POST -H "Content-Type: application/json" -D "{"id": 12345}" http://localhost:8080/async/addgeo

        4. You will get back a UUID as a response from step 1, use that UUID to call the getresults endpoint:
            curl http://localhost:8080/async/getresults/e176cec2-30e1-45d8-8cc1-9fb06bbd4491

        5. You will get back one of two possible responses:
            a. "nothing available yet, try again later"
            b. "Added geo to requested media plan"

        6. Repeat step 3 as necessary, it will take 45 seconds before data is available
