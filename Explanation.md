# Lucky Draw Gaming Service

### Meghna Jakhar <180417> IIT Kanpur
<br>

## Description
This project is done in JAVA language with the following tech. stack.
* Database: <b>MySQL</b>
* Frameworks: <b>Spring Boot</b>
* API Testing : <b>Postman</b>

## API details

* 1st API <br>
    <b>POST</b> : localhost:8000/api/ticketDetails <br>

    <b>Request Body</b> : ``` {"name": "Meghna",
                    "phoneNum": "1234567812",
                    "email": "qwerty@iitk.ac.in",
                    "age": 21
                     }
                     ```
    
    <b>Response</b> : ``` {"ticketId": "10"
                     }
                     ```

    * API which gives user the raffle ticket <br>
      * This API updates the data given by the user in the ticketDetailsRepository generating an automated ticketId and returning it back to the user.
      
<br>

* 2nd API <br>
    <b>GET</b> : localhost:8000/api/nextEventTime <br>

    <b>Body</b> : { }

    <b>Response</b> : ``` {"eventDateTime": , "prize": 
                     }
                     ```


    * This API shows the nextLucky Draw Event timing and the corresponding prize of the event. <br>
      * A currentDateTime variable of localDateTime type is made.
      *  We iterate through the elements of EventDetails Entity Class and compare the dateTime variable of localDateTime type of each element with the currentDateTime variable. If the dateTime is after the currentDateTime, then store it in a array list. 
      * In the end, sort the array list in ascending order and return the smallest element(i.e. the first element) of the array list. 
      * We get the corresponding values of event of the resultDateTime by calling a findByDate method made in the EventDetailsRepository. API returns the prize of that event along with the dateTime. 

* 3rd API <br>
    <b>POST</b> : localhost:8000/api/register/{eventId}/{ticketId} <br>

    <b>Body</b> : { }

    <b>Response</b> : ``` "Success"
                     ```

    * This API allows users to participate in the event. 
      * It takes TicketID and EventID as the input from the user and add the ticketId in the array of the participants in eventDetailsRepository corresponding to that eventId .
      * If the ticketId already exists in the array of the participants corresponding to that eventId, then it will show the error message and won't register the ticketId in the event.
      * If a user has participated in the event with a different ticket, then also it will show the error message. It will compare the names of all the users that are already participating with the current user. If the name matches,it will not allow the user to participate.


* 4th API <br>
    <b>GET</b> : localhost:8000/api/listWinners<br>

    <b>Body</b> : { }

    <b>Response</b> : ``` {"winners": [w1 w1, ....] 
                     }
                     ```

    * This API lists all the winners of all the events in the last one week.
      
      * We iterate through all the dates of the events and store the dates in the array list that lie between today and a week before today.
      * We then access the winners of the events that were held at that time and store them in a list and return that list as the response to this API.

* 5th API <br>
    <b>GET</b> : localhost:8000/api/computeWinner/{eventId} <br>

    <b>Body</b> : { }

    <b>Response</b> : ``` {"name": "someName"
                     }
                     ```

    * This API computes the winner of the event.
       
       * We obtain a random number from all the indexes of the participants array of EventDetails and return the value of the array at that index as the winner ticketID.
       * We retrieve the details from the winner ticketID about the user and save the details of user and event in a winnerDetailsRepository. 
    
