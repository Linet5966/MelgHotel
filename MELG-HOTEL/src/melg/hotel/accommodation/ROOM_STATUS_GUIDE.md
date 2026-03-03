# Room Status Display - Documentation

## 📊 Overview

The Room Status Panel provides a real-time visual display of all hotel rooms and their current booking status. This helps guests see which rooms are available before proceeding with their booking.

## 🎯 Features

### Room Status States

The system displays three room statuses:

1. **Available** (Green ✅)
   - Room is not booked
   - Guest can select this room type for booking
   - Shows current nightly rate

2. **Booked** (Red ❌)
   - Room is currently reserved by another guest
   - Cannot be booked during reserved dates
   - Shows nightly rate

3. **Not Reserved** (Yellow ⚠️)
   - Room exists but has no current bookings
   - Intermediate status between availability checks
   - Shows nightly rate

### Room Organization

Rooms are organized by type:
- **VIP Rooms**: ₦15,000 per night
  - Example: VIP-101, VIP-102, VIP-103

- **Regular Rooms**: ₦8,000 per night
  - Example: REG-201, REG-202, REG-203, REG-204

## 🖼️ Visual Layout

```
┌────────────────────────────────────────────────────────────┐
│              Room Status & Availability                     │
├────────────────────────────────────────────────────────────┤
│  Legend:  [●] Available   [●] Booked   [●] Not Reserved    │
├────────────────────────────────────────────────────────────┤
│  VIP Rooms (₦15,000/night)                                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                  │
│  │ VIP-101  │  │ VIP-102  │  │ VIP-103  │                  │
│  │ Available│  │  Booked  │  │ Available│                  │
│  │₦15,000   │  │₦15,000   │  │₦15,000   │                  │
│  └──────────┘  └──────────┘  └──────────┘                  │
│                                                             │
│  Regular Rooms (₦8,000/night)                               │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │ REG-201  │  │ REG-202  │  │ REG-203  │  │ REG-204  │   │
│  │ Available│  │NotReserved  │ Available│  │Available │   │
│  │₦8,000    │  │₦8,000    │  │₦8,000    │  │₦8,000    │   │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘   │
└────────────────────────────────────────────────────────────┘
```

## 🔧 Technical Details

### RoomStatusPanel.java

Main class responsible for displaying room status.

**Key Methods:**

1. **`loadRoomStatus()`**
   - Loads room data from database
   - Automatically creates sample rooms if database is empty
   - Groups rooms by type

2. **`loadRoomsFromDatabase()`**
   - Queries hotel_rooms table
   - Checks for active bookings
   - Retrieves room type, number, price, and status

3. **`displayRooms()`**
   - Organizes rooms by type (VIP, Regular)
   - Creates visual grid layout
   - Displays status badges with color coding

4. **`refreshRoomStatus()`**
   - Updates room status display
   - Call this to see real-time changes
   - Useful after booking confirmation

5. **`getAvailableRooms()`**
   - Returns list of all available rooms
   - Useful for filtering room options

6. **`getBookedRooms()`**
   - Returns list of booked rooms
   - Useful for reporting

### Color Coding

| Status | Color | RGB Value |
|--------|-------|-----------|
| Available | Green | rgb(100, 200, 100) |
| Booked | Red | rgb(255, 100, 100) |
| Not Reserved | Yellow | rgb(200, 200, 100) |

## 📡 Database Integration

### Tables Used

**hotel_rooms**
```sql
id INT PRIMARY KEY
room_number VARCHAR(10)
room_type VARCHAR(50) -- 'VIP' or 'Regular'
price DOUBLE
status VARCHAR(20) -- 'Available' or 'Not Reserved'
```

**hotel_bookings**
```sql
id INT PRIMARY KEY
room_id INT FOREIGN KEY
guest_name VARCHAR(100)
check_in_date DATE
check_out_date DATE
status VARCHAR(20) -- 'Booked' or 'Cancelled'
```

### Status Query Logic

The system uses this query to determine real-time status:

```sql
CASE WHEN EXISTS (
    SELECT 1 FROM hotel_bookings b 
    WHERE b.room_id = r.id AND b.status = 'Booked'
) THEN 'Booked' ELSE r.status END
```

This checks if a room has any active bookings.

## 🚀 Usage

### Automatic Display
- Room status panel appears automatically when the Accommodation page loads
- Shows all rooms organized by type with current status

### Manual Refresh
To update room status after a booking:

```java
roomStatusPanel.refreshRoomStatus();
```

### Getting Available Rooms
```java
List<Map<String, Object>> available = roomStatusPanel.getAvailableRooms();
for (Map<String, Object> room : available) {
    System.out.println("Room: " + room.get("room_number") + 
                      " - Price: " + room.get("price"));
}
```

### Getting Booked Rooms
```java
List<Map<String, Object>> booked = roomStatusPanel.getBookedRooms();
System.out.println("Total booked rooms: " + booked.size());
```

## 🛠️ Customization

### Change Room Prices

Edit the `ensureSampleRooms()` method:

```java
// For VIP rooms
insertPstmt.setDouble(3, 15000.0); // Change this value

// For Regular rooms
insertPstmt.setDouble(3, 8000.0); // Change this value
```

### Add More Rooms

In `ensureSampleRooms()` method, modify the loop count:

```java
// Create 5 VIP rooms instead of 3
for (int i = 1; i <= 5; i++) {
    // ... insert code ...
}
```

### Change Room Type Names

Edit the room type strings:

```java
insertPstmt.setString(2, "VIP");        // Change naming
insertPstmt.setString(2, "Regular");    // Change naming
```

### Update Status Colors

Modify the color constants in `createRoomCard()`:

```java
if ("Available".equals(status)) {
    statusLabel.setForeground(new Color(100, 200, 100)); // Change green
}
```

## 📋 Sample Data

On first run, the system creates:

**VIP Rooms:**
- VIP-101 (Available, ₦15,000)
- VIP-102 (Booked, ₦15,000)
- VIP-103 (Available, ₦15,000)

**Regular Rooms:**
- REG-201 (Available, ₦8,000)
- REG-202 (Not Reserved, ₦8,000)
- REG-203 (Available, ₦8,000)
- REG-204 (Available, ₦8,000)

## 🔗 Integration Points

### In AccommodationViewPanel.java

```java
// Room Status Panel - Shows availability
RoomStatusPanel roomStatusPanel = new RoomStatusPanel();
mainPanel.add(roomStatusPanel);
```

The panel is displayed immediately after the page title and before the booking form, giving guests clear visibility of available options.

## ✅ Features Checklist

- [x] Real-time room status display
- [x] Color-coded status badges
- [x] Room organization by type
- [x] Legend for status indicators
- [x] Database integration
- [x] Automatic sample data creation
- [x] Refresh functionality
- [x] Query methods for available/booked rooms
- [x] Price display per room
- [x] Grid layout optimized for viewing

## 🐛 Troubleshooting

### Issue: All rooms showing "Not Reserved"
**Solution**: Wait for database sync or manually run:
```java
roomStatusPanel.refreshRoomStatus();
```

### Issue: Sample rooms not created
**Solution**: Check MySQL connection and database permissions

### Issue: Incorrect status showing
**Solution**: Check hotel_bookings table for active bookings (status = 'Booked')

## 📊 Statistics

The room status panel can be extended to show:
- Total rooms count
- Available rooms count
- Occupancy rate
- Booking revenue

Example:
```java
int total = rooms.size();
int available = getAvailableRooms().size();
int occupancy = (int) ((total - available) * 100 / total);
System.out.println("Occupancy: " + occupancy + "%");
```

## 🔄 Real-Time Updates

For real-time room status updates:

1. **Auto-Refresh**: Add timer to refresh every 30 seconds
```java
Timer timer = new Timer(30000, e -> roomStatusPanel.refreshRoomStatus());
timer.start();
```

2. **On Booking**: Refresh after successful booking
```java
if (bookingSuccessful) {
    roomStatusPanel.refreshRoomStatus();
}
```

3. **Manual Refresh**: Add button for users to refresh
```java
refreshButton.addActionListener(e -> roomStatusPanel.refreshRoomStatus());
```

---

**Last Updated**: March 2026  
**Component**: RoomStatusPanel.java  
**Status**: Complete and Integrated
