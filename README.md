## Conference Room Simulation

The code tries to do a simple simulation of a room in a conference. The program is inspired and an edited version of the CMPLXSY Seating Simulation.

## Rules

1. If all attendees (turtles) find their location to rate the conference as being exceptional, then stop the simulation.
2. Exceptionality is having more Moore-neighbors that has higher level of expertise than them compared to equal or lower level of expertise than them(except with Top (T))
    1. Top (T) attendee find it exceptional to be another Top (T) attendee.
3. If an attendee don’t find his/her location exceptional, then find a new spot.

## **The reasoning behind the rules**

- Attendees have more complicated motivations and reasons for attending a conference. This is a simplification that conference attendees want to learn; hence they will find it more exceptional if they are near attendees with higher expertise than them. (and equal for Top (T) attendees)
- Moreover, the equal or lower level of expertise of Moore neighbors will lower the exceptionality rating for the attendees as they will be their competition to talk to attendees of higher expertise. Moreover, attendees have limited time, and entertaining a lower level of expertise will lessen the time they have for their own personal gains.

## Data

| Density | 20 | 40 | 60 | 80 |
| --- | --- | --- | --- | --- |
| Beginner (B) | 0 | 0 | 0 | 34 |
| Middle (M) | 0 | 32 | 36 | 81 |
| Top (T) | 0 | 0 | 0 | 2 |
| Ticks | 15 | 100000 | 100000 | 100000 |

(Due to simulation not stopping, the developer decided to stop the loop at 100000 ticks)
## Insights

- There is a noticeable gap that Middle (M) attendees will not find the conference exceptional. In contrast, Beginner (B) and Top (T) find it easier to get a position and have an exceptional conference.
- Density 20 seem a good spot to set density especially for Middle (M). As density reach 40 and higher, it became harder for Middle (M) to have the exceptional spot.
- After reaching density 80, it became also harder for Beginner (B) and Top (T) attendees to find the exceptional location for them.

## Image

Density: 50 

### Before
<img width="446" alt="Screenshot 2023-01-30 at 4 10 20 AM" src="https://user-images.githubusercontent.com/62783701/215353579-a9ba46e5-7a75-4cee-bf0a-cc4b2d403f5e.png">

### After 100000 ticks
<img width="433" alt="Screenshot 2023-01-30 at 4 12 22 AM" src="https://user-images.githubusercontent.com/62783701/215353598-4df72f8b-1b84-4988-b640-e063b98ed299.png">
