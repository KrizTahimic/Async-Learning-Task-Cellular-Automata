### Conference Room Simulation

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

## Insights

There is a noticeable gap that Middle (M) attendees will not find the conference exceptional. In contrast, Beginner (B) and Top (T) find it easier to get a position and have an exceptional conference.

## Image

Density: 50 

### Before

![Screenshot 2023-01-30 at 4.10.20 AM.png](Asynch%20Project%201aef0ebc073c42f1b8c3333ad4e3e343/Screenshot_2023-01-30_at_4.10.20_AM.png)

### After 100000 ticks

![Screenshot 2023-01-30 at 4.12.22 AM.png](Asynch%20Project%201aef0ebc073c42f1b8c3333ad4e3e343/Screenshot_2023-01-30_at_4.12.22_AM.png)

# Conference Open room

- [Name & Experience: **1**] - [Population: 25%] -
    - happy with 5 - wants guidance or projet with 5
    - neutral with 10 - (since 1 wants to connect with 10 but at the same time is intimadated)
- [Name & Experience: **5**] - [Population: 70%]
    - happy to 10 (wants advice from 10),
    - happy with 1 - (need help from 1)
- [Name & Experience: **10**] - [Population: 5%] - most popular -
    - happy with 5 (they want more complex/ambitioius discussion and projects, sad with 1)
- Free space to people ratio: <soon to be researched>
- Questions
    - Is this okay?
    - Other things to consider?
    - Advice?
    - Report how it changes.
- Limitatioms
    - not multithreading
    - 

Asuuming equal population

simple model

Blue having a difficult time to find a position to have an exceptional conference

Run 100000 ticks

20 - 15 ticks 

40 - blue hard time - 100000 ticks - 32

60 - less blue - 36

80 - 2 unhappy violet - 34 green 81 blue unexceptional

hate bec competition and time 

```jsx
; what position in the room would attendees find exceptional
turtles-own [
  exceptional?
  like-nearby
  hate-nearby
  total-nearby
]

to setup
  clear-all

  ; I can implement a let or set here
  ; Implement using ifelse
  ; Set range for using density
  ; Also a slider

  ask patches [
    set pcolor black
    if random 100 < density[
      sprout 1 [
        set color one-of [violet blue green]
        set size 1
      ]
    ]
  ]
  update-turtles
  reset-ticks
end

to go
  if all? turtles [exceptional?] [stop]
  move-unhappy-turtles
  update-turtles
  tick
end

to move-unhappy-turtles
  ask turtles with [ not exceptional? ]
  [ find-new-spot ]
end

to find-new-spot
  rt random-float 360
  fd random-float 10
  if any? other turtles-here [ find-new-spot ]
  move-to patch-here
end

to update-turtles
  ask turtles [

    ; Beginner (B)
    ; B- M+ T+
    if color = green [
      set like-nearby count (turtles-on neighbors) with [color = blue or color = violet]
      set hate-nearby count (turtles-on neighbors) with [color = green]
    ]
    ; Middle (M)
    ; B- M- T+
    if color = blue [
      set like-nearby count (turtles-on neighbors) with [color = violet]
      set hate-nearby count (turtles-on neighbors) with [color = blue or color = green]
    ]
    ; else voilet
    ; Top (T)
    ; B- M- T+
    if color = violet [
      set like-nearby count (turtles-on neighbors) with [color = violet or color = blue]
      set hate-nearby count (turtles-on neighbors) with [color = green]
    ]

    ; Will be used
    set total-nearby like-nearby + hate-nearby
    set exceptional? like-nearby >= (50 * total-nearby / 100)
    ifelse exceptional? [set shape "square"] [set shape "X"]
  ]
end
```
