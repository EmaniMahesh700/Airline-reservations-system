# Airline-reservations-system
The airline reservations system is a java-based application designed to manage airline  reservation,flights,and passengers. The system allows users to search for flights,book tickets,ad manage their reservations.The system also provides an admin panel for managing flights,reservations, and users.
class Flight {
  constructor(flightNumber, departure, arrival, seats) {
    this.flightNumber = flightNumber;
    this.departure = departure;
    this.arrival = arrival;
    this.seats = seats;
    this.reservations = [];
  }

  reserveSeat(passengerName) {
    if (this.seats > 0) {
      this.seats--;
      this.reservations.push(passengerName);
      return Seat reserved for ${passengerName} on flight ${this.flightNumber};
    } else {
      return No seats available on flight ${this.flightNumber};
    }
  }

  cancelReservation(passengerName) {
    const index = this.reservations.indexOf(passengerName);
    if (index !== -1) {
      this.seats++;
      this.reservations.splice(index, 1);
      return Reservation cancelled for ${passengerName} on flight ${this.flightNumber};
    } else {
      return No reservation found for ${passengerName} on flight ${this.flightNumber};
    }
  }
}

class AirlineReservationSystem {
  constructor() {
    this.flights = [];
  }

  addFlight(flightNumber, departure, arrival, seats) {
    this.flights.push(new Flight(flightNumber, departure, arrival, seats));
  }

  reserveSeat(flightNumber, passengerName) {
    const flight = this.flights.find(f => f.flightNumber === flightNumber);
    if (flight) {
      return flight.reserveSeat(passengerName);
    } else {
      return Flight ${flightNumber} not found;
    }
  }

  cancelReservation(flightNumber, passengerName) {
    const flight = this.flights.find(f => f.flightNumber === flightNumber);
    if (flight) {
      return flight.cancelReservation(passengerName);
    } else {
      return Flight ${flightNumber} not found;
    }
  }

  displayFlights() {
    console.log("Available Flights:");
    this.flights.forEach(flight => {
      console.log(Flight Number: ${flight.flightNumber});
      console.log(Departure: ${flight.departure});
      console.log(Arrival: ${flight.arrival});
      console.log(Seats: ${flight.seats});
      console.log(Reservations: ${flight.reservations.length});
      console.log("------------------------");
    });
  }
}

const ars = new AirlineReservationSystem();

ars.addFlight("AA101", "New York", "Los Angeles", 200);
ars.addFlight("AA102", "Los Angeles", "New York", 200);

console.log(ars.reserveSeat("AA101", "John Doe"));
console.log(ars.reserveSeat("AA101", "Jane Doe"));
console.log(ars.cancelReservation("AA101", "John Doe"));
ars.displayFlights();
