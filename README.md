# G103 — Team Alpha Omega

Gruppeprosjekt i **IBE160 Programmering med KI** ved Høgskolen i Molde, høsten 2026 (15 studiepoeng).

Repoet inneholder gruppens applikasjon og dokumentasjon av utvikling, testing og kvalitetssikring med KI.

## Medlemmer

- Bjornar Berge
- Tomas Hagen
- Lars Skaufel Holmen
- Nhatphong Nguyen



# Product Brief: SimpleTravel — AI-Assisted Travel Planning Platform

## Executive Summary

SimpleTravel is a web application that helps users plan a complete trip in one place.

Planning a trip often requires users to switch between several different services for weather forecasts, transportation, accommodation, restaurants, events, activities, maps, packing lists, and budgeting. This can make travel planning time-consuming and difficult to organize.

SimpleTravel aims to simplify this process by collecting the most important travel information into one platform. The user chooses a destination, travel dates, trip duration, interests, budget, and preferred transport method. The application then helps create a personalised travel plan.

An AI assistant supports the planning process by suggesting activities, creating a daily itinerary, estimating costs, recommending what clothes to bring, and generating a packing list based on destination, season, weather, and planned activities.

The goal is not to replace existing travel services, but to give the user one central place where the entire trip can be planned and organised.

---

## The Problem

Planning a trip usually requires information from many different websites and applications.

A traveller may need to use:

- Google Maps for routes
- weather applications for forecasts
- airline websites for flights
- restaurant services for food
- event websites for concerts or sports
- travel websites for attractions
- notes or calendars to create an itinerary
- separate tools to calculate the travel budget

This creates a fragmented planning experience.

It can also be difficult for travellers to answer practical questions such as:

- What activities are available at the destination?
- What will the weather be like?
- What clothes should I bring?
- How much will the trip approximately cost?
- What events are happening while I am there?
- Is the destination crowded during this season?
- How should I organise each day?
- What should I pack?
- What is the best way to travel between different places?

For users who do not know the destination well, finding and organising all this information can require significant time and research.

---

## The Solution

SimpleTravel provides one travel-planning dashboard where the user can create and manage a trip.

The user starts by entering basic information:

- destination
- travel dates
- number of days
- budget
- interests
- transportation preference
- number of travellers

The platform then creates a central trip overview.

### AI Travel Assistant

An AI assistant helps the user create a personalised travel plan.

For example, the user could ask:

> "I am travelling to Barcelona for four days in October. I like football, local food and museums. My budget is €700."

The AI assistant could then suggest:

- activities
- restaurants
- tourist attractions
- events
- transportation
- a daily schedule
- estimated costs
- clothing recommendations
- a packing list

The user can modify the plan by continuing the conversation with the assistant.

For example:

> "Make day two cheaper."

or:

> "Replace the museum with an outdoor activity."

The itinerary can then be automatically updated.

---

## Core Features

### Trip Creation

Users can create a trip by entering:

- destination
- start and end date
- trip duration
- number of travellers
- approximate budget
- interests

The trip is saved so the user can return to it later.

### Daily Itinerary

The application creates a day-by-day schedule.

Example:

**Day 1**

09:00 — Breakfast  
10:00 — City sightseeing  
13:00 — Lunch  
14:30 — Museum  
18:00 — Hotel/rest  
20:00 — Restaurant  

Users can manually change activities or ask the AI assistant to reorganise the schedule.

### Weather

Weather information for the destination is displayed together with the itinerary.

Weather can influence recommendations.

For example, if rain is expected, the system can suggest indoor activities instead of outdoor activities.

### Activities and Places

The platform helps users discover:

- tourist attractions
- museums
- restaurants
- cafés
- landmarks
- nature activities
- shopping
- nightlife

Recommendations can be based on the user's interests.

### Events

The platform can show events happening during the trip, such as:

- concerts
- festivals
- sports events
- cultural events
- exhibitions

These events can be added to the itinerary.

### Transportation

Users can specify how they plan to travel.

Examples include:

- car
- airplane
- public transportation
- walking

The application can show routes between planned activities and help the user understand travel time between locations.

### Cost Estimation

The platform provides an estimated travel budget.

Possible categories include:

- transport
- accommodation
- food
- activities
- events
- other expenses

Example:

| Category | Estimated Cost |
|---|---:|
| Flights | €220 |
| Accommodation | €300 |
| Food | €160 |
| Activities | €80 |
| Local transport | €40 |
| Total | €800 |

The AI assistant can also help the user reduce the cost of the trip.

For example:

> "Reduce my total budget to €650."

The application could then suggest cheaper activities or restaurants.

### Clothing Recommendations

The application recommends clothing based on:

- destination
- weather
- season
- activities

For example:

> Rain expected on Tuesday. Bring a waterproof jacket and suitable shoes.

### Packing List

The application generates a packing list automatically.

Example:

- passport
- phone charger
- travel documents
- shirts
- trousers
- rain jacket
- walking shoes
- toiletries

The user can check items off before travelling.

---

## Seasonal Travel Information

SimpleTravel should help users understand what a destination may be like during the selected travel period.

The application can provide information such as:

- high season
- low season
- typical weather
- expected tourist activity
- important seasonal events

This helps users decide both when to travel and what to expect.

For example:

> July is considered high season in Barcelona and major tourist areas may be crowded.

---

## What Makes This Different

SimpleTravel is not intended to replace Google Maps, airline booking services or restaurant platforms.

Instead, the main advantage is that it combines information from several areas into one personalised travel plan.

### One central travel plan

Instead of keeping information in several applications, the user has one trip dashboard.

### AI-assisted planning

The AI assistant can create and modify the itinerary through natural language.

### Context-aware recommendations

Recommendations can consider several factors at the same time:

- destination
- date
- weather
- budget
- interests
- trip duration

### Practical preparation

The application does not only recommend places to visit. It also helps users prepare through:

- packing lists
- clothing recommendations
- budget calculations
- daily schedules

---

## Who This Serves

### Primary Users

The main target group is people who travel for holidays or short trips and want an easier way to organise their journey.

This could include:

- students
- young adults
- couples
- families
- solo travellers

They may know where they want to travel but not necessarily what they should do when they arrive.

Success for these users means being able to create a useful travel plan quickly without researching many different websites.

### Secondary Users

A secondary target group is people who travel frequently and want a convenient tool for organising several trips.

Examples include:

- digital nomads
- business travellers
- frequent travellers

---

## Success Criteria

### Functional

A user should be able to:

- create a trip
- choose destination and dates
- receive activity suggestions
- generate an AI-assisted itinerary
- view weather information
- see estimated costs
- create a packing list
- receive clothing recommendations
- save and edit the trip

### User Experience

The application should make it possible to create an initial travel plan within a few minutes.

The interface should clearly show:

- upcoming activities
- daily schedule
- expected weather
- estimated costs
- important travel information

### Technical

The application should:

- work in modern desktop and mobile browsers
- store user trips reliably
- provide clear error messages when external services are unavailable
- respond quickly when generating travel recommendations
- protect user account information

---

## Scope

### In Scope for Version 1

The first version will focus on the core travel-planning experience.

Included features:

- user registration and login
- create and save trips
- destination and date selection
- AI travel assistant
- AI-generated itinerary
- activities and attraction suggestions
- weather information
- basic map and route functionality
- cost estimation
- clothing recommendations
- packing list
- editable daily calendar
- responsive web interface

---

## Possible Additional Features

If development time allows, the following features may be added:

- restaurant recommendations
- concerts and event discovery
- sports events
- seasonal crowd information
- more advanced transportation information

---

## Explicitly Out of Version 1

Some ideas from the initial brainstorming are valuable but would make the first version too large.

These are therefore considered future features:

- direct flight booking
- direct hotel booking
- direct Foodora/Wolt ordering
- payment processing
- live airline ticket prices
- advanced public-transport booking
- social matching between travellers
- traveller chat
- full digital-nomad community features

These features may be considered in later versions.

---

## Future Social Feature

One possible future feature is a traveller community inspired by platforms such as Nomad Table.

Users visiting the same destination at approximately the same time could choose to discover other travellers interested in similar activities.

For example:

> "Three other travellers in Barcelona this week are interested in football."

Users could then optionally organise shared activities.

This feature is outside the initial MVP because it introduces additional requirements related to privacy, user communication, moderation and security.

---

## How AI Is Used

Artificial intelligence is a central part of SimpleTravel.

AI can assist with:

- generating travel itineraries
- recommending activities
- reorganising schedules
- suggesting cheaper alternatives
- generating packing lists
- recommending clothing
- summarising destination information
- answering questions about the user's trip

However, the AI does not make decisions automatically.

The user remains in control and can:

- accept recommendations
- reject recommendations
- edit activities
- regenerate individual days
- ask for alternatives

The project will therefore explore how AI can support travel planning while still allowing users to make the final decisions.

---

## Development Approach

The project will follow the Double Diamond design process.

### Discover

The group will investigate problems travellers experience when planning trips.

This includes identifying:

- what information travellers search for
- which applications they currently use
- where planning becomes difficult
- what information is most important

### Define

The group will identify the main problem the application should solve and determine the most important user needs.

### Develop

Different solutions and interfaces will be explored.

The initial Crazy 8 exercise has already produced ideas including:

- weather
- transportation
- activities
- food
- events
- budgeting
- seasonal information
- packing
- clothing recommendations
- AI assistance

These ideas will be evaluated and prioritised.

### Deliver

The most important features will be implemented and tested as a working web application.

AI-assisted programming will be used during development, while the group will review, test and evaluate the generated code.

---

## Vision

The long-term vision for SimpleTravel is to provide one intelligent travel-planning environment where a user can go from:

"I want to travel somewhere"

to

"My entire trip is organised."

Instead of replacing specialised services, SimpleTravel acts as the layer that connects travel information into one personalised plan.

A future version could combine transportation, events, restaurants, booking services and social travel features, allowing the platform to support the traveller before, during and after the journey.
