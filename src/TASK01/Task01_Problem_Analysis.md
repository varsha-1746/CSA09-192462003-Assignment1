# TASK 1 – Problem Analysis and Identification of Objects

## 1. Problem Understanding

The Campus Smart-Parking System is designed to manage vehicle parking in a multi-level university parking facility. The facility is used by students, staff and visitors. It supports two-wheelers, cars and electric vehicles. Electric vehicles may also require special charging slots.

When a vehicle enters the facility, the system checks for a suitable free parking slot, allocates the slot and generates a unique parking ticket. The entry time is recorded. When the vehicle exits, the system calculates the parking fee based on the vehicle type and parking duration, releases the occupied slot and updates the availability.

Students and staff with a valid monthly pass are allowed to park without paying the normal parking fee, whereas visitors must pay the applicable charges.

The main objective is to make parking allocation accurate, prevent duplicate slot usage and maintain proper records of vehicles and payments.

## 2. Inputs and Outputs

### Inputs

- Vehicle registration number.
- Vehicle category (two-wheeler, car or electric vehicle).
- User category (student, staff or visitor).
- Monthly pass details and validity.
- Available floor and slot information.
- Vehicle entry time and exit time.
- Charging slot requirement for electric vehicles.
- Applicable parking rates.

### Outputs

- Allocated floor number and parking slot number.
- Unique parking ticket number.
- Recorded vehicle entry and exit times.
- Total parking duration.
- Calculated parking fee.
- Charging fee, where applicable.
- Updated availability of parking slots.
- Error message when no suitable slot is available or an invalid operation is attempted.

## 3. Candidate Classes and Their Responsibilities

| Candidate Class | Responsibilities | Why It Is Needed |
|---|---|---|
| Vehicle | Stores registration number and vehicle details. | Represents each vehicle as an individual object. |
| TwoWheeler | Represents two-wheeler-specific details and parking rates. | Allows different vehicle categories to have different rules. |
| Car | Represents cars and their applicable parking rates. | Separates car-related behaviour from other vehicles. |
| ElectricVehicle | Represents electric vehicles and charging requirements. | Supports charging-related operations and separate charges. |
| ParkingSlot | Stores slot number, floor, type and availability. | Prevents two vehicles from occupying the same slot. |
| ParkingFacility | Manages floors, slots and parking allocation. | Coordinates the complete parking operation. |
| ParkingTicket | Stores ticket number, vehicle details and entry/exit times. | Maintains a record of each parking transaction. |
| User | Stores user information and category. | Identifies whether the vehicle belongs to a student, staff member or visitor. |
| MonthlyPass | Stores pass validity and holder information. | Checks whether a student or staff member is eligible for free parking. |

These classes are justified because each represents a separate entity or responsibility in the parking system. Separating vehicle types also makes it easier to introduce additional categories without placing all the logic inside one large class.

## 4. Nouns and Verbs Identified from the Problem

### Nouns – Candidate Classes or Attributes

Parking facility, floor, slot, vehicle, two-wheeler, car, electric vehicle, user, student, staff, visitor, parking ticket, registration number, entry time, exit time, parking fee, charging slot and monthly pass.

### Verbs – Candidate Methods

- allocateSlot() – Assigns a suitable free parking slot.
- releaseSlot() – Makes an occupied slot available.
- generateTicket() – Creates a new parking ticket.
- recordEntryTime() – Records when a vehicle enters.
- recordExitTime() – Records when a vehicle leaves.
- calculateDuration() – Calculates the total parking duration.
- calculateFee() – Computes the parking charge.
- validatePass() – Checks monthly pass validity.
- checkAvailability() – Checks whether a suitable slot is free.
- calculateChargingFee() – Calculates the EV charging charge.

## 5. Business Rules

1. A parking slot can contain only one vehicle at a time.
2. A vehicle must be assigned only to a suitable slot.
3. Every parking ticket must have a unique ticket number.
4. A ticket number must never be reused.
5. The vehicle registration number must be recorded correctly.
6. A vehicle must have a valid entry record before its exit can be processed.
7. A slot must be released after the vehicle exits.
8. The parking fee must depend on the vehicle category and parking duration.
9. Students and staff with a valid monthly pass are exempt from the normal parking fee.
10. Visitors must pay the applicable parking fee.
11. Electric vehicles requiring charging must be assigned suitable charging slots.
12. A vehicle cannot be allocated another slot while its existing parking session is active.

## 6. Assumptions

- Each vehicle has a unique registration number.
- Each floor has a fixed number of parking slots.
- Slot numbers are unique within their respective floors.
- Parking rates are predefined by the university.
- Entry and exit times are recorded using the system clock.
- Monthly passes are valid only for their specified validity period.
- Charging slots are limited and can be used only by eligible electric vehicles.
- The system processes one parking entry or exit operation at a time.
- A vehicle must have an active parking ticket to complete an exit operation.

## 7. Alternative Concept – Objects vs Parallel Arrays

In the object-oriented design, every vehicle is represented by a separate Vehicle object. Its registration number, vehicle type and entry time are stored together as fields inside that object.

An alternative approach is to store the same information in parallel arrays:

- regNo[] – Stores vehicle registration numbers.
- type[] – Stores vehicle categories.
- entryTime[] – Stores entry times.

For example, the vehicle information at index 0 in all three arrays belongs to the same vehicle.

### Finding a Vehicle by Registration Number

In the object-oriented approach, the system searches through the collection of Vehicle objects and compares each object's registration number.

In the parallel-array approach, the system searches the regNo[] array and uses the matching index to retrieve the corresponding type and entry time from the other arrays.

Both approaches require a linear search.

### Adding a New Vehicle Attribute

In the object-oriented approach, a new attribute can be added as a field in the Vehicle class. The related constructor and methods can then be updated where necessary.

In the parallel-array approach, a new array must be created for the additional attribute. Every insertion, deletion and update must maintain the same index across all arrays. This increases the possibility of mismatched data.

### Complexity Comparison

| Operation | Vehicle Objects | Parallel Arrays |
|---|---|---|
| Search by registration number | O(n) | O(n) |
| Retrieve vehicle details after search | O(1) | O(1) using the matched index |
| Add a new attribute | Update the class and relevant logic | Add another array and maintain matching indexes |
| Storage per vehicle | Object reference and object fields, with object overhead | One reference in each parallel array |

Here, n represents the number of parked vehicles.

The search time is O(n) in both approaches. The object-oriented approach may use additional memory for object overhead, but it keeps related data and behaviour together. Parallel arrays may use less per-record structural overhead, but maintaining consistent indexes becomes difficult as the system grows.

## 8. Conclusion

The object-oriented approach is more suitable for the Campus Smart-Parking System because the system contains several related entities with different responsibilities and behaviours. Using separate classes improves readability, maintainability and extensibility. It also makes it easier to introduce new vehicle categories, parking rules and charging facilities in the future.

Therefore, an object-oriented design is preferred over parallel arrays for this system.
