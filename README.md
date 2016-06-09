#### This directory contains docker sources of a few sample WSO2 demos ####

**Environment Setup**
	
  1. Add a host entry to the host machine
     - `docker machine start` - will start the docker machine if you are using `windows` or `OSx`.
     - `docker machine ip` - will display the IP address of the docker machine.
     - Open the `hosts` file of the host machine, and add an entry as `<ip-address> docker.machine`.
  2. Download and add the required binary packs.
     - Open the README.md file inside service/pack and follow the instructions
     - Open the README.md file inside esb/pack and follow the instructions

**Sample SOAP backend service**

  1. Start the service container
     - `docker-compose up -d service` - will create the SOAP service container image and boot it up
     - `docker ps` - lists the running container information. 
     - Observe the NAME value ( stocks.example.com ) of the container
  2. Try it
     - Open SOAPUI
     - Add [http://docker.machine:9000/services/SimpleStockQuoteService?wsdl](http://docker.machine:9000/services/SimpleStockQuoteService?wsdl)
     - Try the operation `getQuote` providing a Symbol value
     
**ESB**

  1. Start the esb container
     - `docker-compose up -d esb` - will create the ESB container image and boot it up
  2. Tail ESB logs (and observe output each time you execute an action)
     - `docker exec -it esb.example.com tailf wso2/wso2esb-4.9.0/repository/logs/wso2carbon.log`
  3. Login to the web based admin management console
     - use `admin` and `admin` as username and password
     - Open [https://docker.machine:9444/carbon](https://docker.machine:9444/carbon)
  4. Upload the CAR file (artifacts)
     - Go to `Main > Manage > Carbon Applications > Add`
     - Upload `articats/0002BasicCARProject_1.0.0.car` file
     - Observe ESB logs
  5. Observe the artifacts uploaded on the admin management console
     - API : `Main > Manage > APIs`
     - Endpoint : `Main > Manage > Endpoints`
     - Sequences : `Main > Manage > Sequences`
     
**Run the sample**

  1. Start a REST client like [POSTMAN](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en)
  2. Add `http://docker.machine:8281/stocks/quote/<any symbol>`
     - i.e. `http://docker.machine:8281/stocks/quote/WSO2`
  3. Invoke and observe the response
  4. Add header `Accept` with value `application/json`
  5. Invoke and observe the response
  