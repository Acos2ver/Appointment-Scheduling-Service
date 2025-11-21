# Appointment Scheduling Service

A microservice for booking appointments and managing appointment time slot reservations.

## Overview

This microservice provides functionality for customers to view available time slots, book appointments, and receive confirmation notifications. It implements optimistic locking to ensure data integrity and guarantees reliable message delivery for appointment confirmations.

## Features

### User Story 1: Book Resource Time Slot
As a customer, I want to view available dates/times and schedule a specific appointment for a required resource so that I can select a reservation that fits my personal schedule.

**Key Capabilities:**
- View available time slots for specific resources
- Book appointments with immediate reservation
- Optimistic locking mechanism to prevent double-booking
- Data integrity and correctness guarantee

### User Story 2: Receive Appointment Confirmation
As a customer, I want to receive an immediate notification via email confirming the details of my scheduled appointment so that I have a verified record of the date and time.

**Key Capabilities:**
- Automatic confirmation message generation
- Integration with notification service queue
- At-least-once delivery guarantee for reliability
- Asynchronous notification processing

## API Endpoints

### Health Check
```
GET /health
```
Returns service health status.

**Response:**
```json
{
  "message": "Appointment Scheduling Microservice Online"
}
```

### Get Available Slots
```
GET /api/slots/available?resource_id={resource_id}
```
Retrieves available time slots for a specific resource.

**Query Parameters:**
- `resource_id` (string, required): The ID of the resource

**Response:**
```json
{
  "message": "Available slots endpoint",
  "resource_id": "resource123",
  "available_slots": []
}
```

### Book Appointment
```
POST /api/appointments
```
Books a new appointment for a customer.

**Request Body:**
```json
{
  "customer_id": "customer123",
  "resource_id": "resource456",
  "date": "2024-12-15",
  "time": "14:00"
}
```

**Response:**
```json
{
  "message": "Appointment booked successfully",
  "appointment_id": "appt789",
  "customer_id": "customer123",
  "resource_id": "resource456",
  "date": "2024-12-15",
  "time": "14:00",
  "status": "confirmed"
}
```

### Confirm Appointment
```
POST /api/appointments/confirm
```
Sends appointment confirmation to notification service.

**Request Body:**
```json
{
  "appointment_id": "appt789"
}
```

**Response:**
```json
{
  "message": "Confirmation sent to notification service",
  "appointment_id": "appt789",
  "notification_status": "queued"
}
```

### Get Appointment Details
```
GET /api/appointments/{appointment_id}
```
Retrieves details of a specific appointment.

**Response:**
```json
{
  "message": "Appointment details",
  "appointment_id": "appt789"
}
```

## Setup and Installation

### Prerequisites
- Python 3.9 or higher
- pip

### Local Development

1. **Clone the repository:**
```bash
git clone 
cd Appointment-Scheduling-Service
```

2. **Install dependencies:**
```bash
pip install -r requirements.txt
```

3. **Run the service:**
```bash
python app.py
```

The service will start on `http://localhost:5006`

### Docker Deployment

1. **Build the Docker image:**
```bash
docker build -t appointment-scheduling-service .
```

2. **Run the container:**
```bash
docker run -p 5006:5006 appointment-scheduling-service
```

3. **Verify the service is running:**
```bash
curl http://localhost:5006/health
```

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Port number for the service | `5006` |
| `CORS_ORIGINS` | Comma-separated list of allowed CORS origins | `http://localhost:5173,http://localhost:5000` |

## Architecture

### Quality Attributes

**Integrity:**
- Implements optimistic locking mechanism
- Prevents concurrent booking conflicts
- Ensures data correctness and completeness

**Reliability:**
- At-least-once delivery guarantee for notifications
- Message queue integration for asynchronous processing
- Resilient to temporary notification service unavailability

## Technology Stack

- **Framework:** Flask 3.0.0
- **CORS Support:** Flask-Cors 4.0.0
- **Environment Management:** python-dotenv 1.0.0
- **Containerization:** Docker

## Team

- **Lev:** Main Implementation
- **Olivia:** Collaborator

## Development Status

This is the initial setup with placeholder endpoints. Full implementation including:
- Database integration
- Optimistic locking mechanism
- Message queue integration
- Complete business logic

will be added by the main developer.

## License

[Add your license information here]
