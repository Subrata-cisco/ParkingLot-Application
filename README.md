# ParkingLot-Application

# Getting Started
1. Import the Spring Boot application in eclipse.
2. We can use maven clean install to build it.

### Command that can tried on command prompt (Note click the console before giving the following commands)

1. pc create-parking --site mall --vehicle motorcycle car bus --spot 2 10 20

2. pc park --vt bike

3. pc park --vt motorcycle

4. pc park --vt motorcycle

5. pc park --vt motorcycle

6. pc unpark --vt motorcycle --tn "0000002"

7. pc park --vt motorcycle


8. pc create-parking --site airport --vehicle motorcycle car bus --spot 5 1 20

9. pc park --vt car

10. pc park --vt car

11. pc unpark --vt car --tn "0000001"

12. pc park --vt car

### Test case covers the 38 use cases on important aspects of the application.
1. Park/Unpark is happening correctly.
2. Fee's are calculated correctly for Flat and interval type of billing.
3. Few mandatory validations.

#### Limitation of the Application.
1. The actual customer application might be totally different , this just conveys my mental model on low level software design thinking.
2. Instead of command line application i could have designed it as rest service.
3. The application needs more iteration and thinking to design it better.
4. Create new object instead of injecting the dependency in many places was not possible due to airlift command line interface not understanding spring framework (rest application would have injected nicely.)
5. Saving the data temporarily in the application cache instead of any database activity.
5. More test cases would be possible but focused on core use cases (due to lack of time , can't afford putting more time than 25 hours that i gave for this project for apart from my office work)
6. Could not do extensive testing due to lack of time.
7. Wanted to build the build the application using Gradle but encountered an issue with my laptop so ended up building it using maven.
8. Airlift CLI framework is not maintained anymore , would not use it for any purpose , because of earlier experience used it for speed of development.

#### How to read the code
1. ParkinglotApplication is the main program that runs.
2. ParkingLotCommand is the class which understand all the command for create/park/unpark command. (all java files under com.sahaj.parkinglot.cli does the command line parsing work )
3. CreateParkingCommand,ParkVehicleCommand,UnParkVehicleCommand initiates the creating parking lot , parking and unparking. (package com.sahaj.parkinglot.cli.command is dedicated for it.)
4. ParkingLotManager and ParkingService contain the business logic for park/unpark. 
5. com.sahaj.parkinglot.fee package is responsible for calculating the flat and interval fees for different sites.
  (DailyFeeCalculator , HourlyFeeCalculator , FlatFeeCalculator and respective *Retriver.java does the math)

6.GlobalStore file maintain all the data required to run this application. We could have design the strategy class to handle the volatile and future persistent store but did not go it.

7.util package has business logic to check and persist the data in the local cache GlobalStore.

8. AirportTypeIntervalFeeData ,StadiumTypeIntervalFeeData , FlatFeeData are the hard coded configuration information about fee models.
