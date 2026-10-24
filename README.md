EventHub
--
A Django REST Framework based ticket reservation API for a simplified event ticketing platform.

Structure of my Folder:
```
eventhub/
├── manage.py
├── eventhub/
│   ├── settings.py
│   └── urls.py
├── events/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   ├── middleware.py
│   └── migrations/
├── db.sqlite3 (Hidden)
└── requirements.txt
```
Installation and running:
--
```
git clone <repo-url>
cd eventhub
pip install -r requirements.txt
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
```
Design Decision: 
--
Seat deduction is performed inside the ReservationSerializer create() method. 
This keeps reservation creation and seat updates together, reducing the chance of inconsistent data and centralising reservation business logic.

Testing CheckList: (postman)
--
Create an event:
POST - http://127.0.0.1:8000/api/events/

List all events:
GET - http://127.0.0.1:8000/api/events/

Filter events by status
GET - http://127.0.0.1:8000/api/events/?status = ongoing

Filter events by venue
GET - http://127.0.0.1:8000/api/events/?venue = hyderabad

Create a reservation (seats deducted from event)
POST - http://127.0.0.1:8000/api/reservations/

Filter reservations by event_id
GET - http://127.0.0.1:8000/api/reservations/?event_id = 3

Overbooking attempt returns 400 - Success 
--
<img width="1591" height="1050" alt="Aoverseats" src="https://github.com/user-attachments/assets/c32cf92f-8ec8-46bc-8a15-9d782d4706c7" />

Cancel a reservation (seats restored to event) - Success
--
<img width="1432" height="1039" alt="cancel Reservation" src="https://github.com/user-attachments/assets/125405b6-4b6f-40f5-9864-226bb0b2a1ec" />


Middleware logs appear in the terminal for every request - Success
--
<img width="1555" height="869" alt="Middlewarelogs" src="https://github.com/user-attachments/assets/8bfd64e0-bf74-4260-b46e-830e7dccfa19" />

Successful reservation (201 Created) 
--
<img width="1398" height="912" alt="resSuccess" src="https://github.com/user-attachments/assets/9c024b6e-e35e-4f97-a8e3-fd8a9da4cd6b" />

Overbooking failure (400 Bad Request)
--
<img width="1591" height="1050" alt="Aoverseats" src="https://github.com/user-attachments/assets/619dffe3-63dd-401d-bad3-4e4e6654a7a4" />

Successful cancellation
--
<img width="1432" height="1039" alt="cancel Reservation" src="https://github.com/user-attachments/assets/d29cc9a8-5fd9-437f-a578-a48da1d8fe25" />

Final Checklist:
--
```
1) Event model implemented
2) Reservation model implemented
3) ForeignKey relationship satisfied
4) SerializerMethodField 
5) Event validation and Reservation validation
6) Seat deduction on reservation
7) Event filtering by `status`
8) Event filtering by `venue`
9) Reservation filtering by `event_id`
10) CANCEL action
11) Seat restoration on cancellation
12) Router configuration
13) Middleware logging
14) All endpoints match assignment requirements as mentioned
```
