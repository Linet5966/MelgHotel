# Accommodation Module - Quick Reference

## 📁 Folder Structure

```
src/melg/hotel/accommodation/
├── AccommodationViewPanel.java              # Main UI form panel
├── PaymentPanel.java                        # Payment method selection
├── FamilyPicturesPanel.java                 # Image gallery
├── AccommodationDatabaseHelper.java         # Database operations
├── README.md                                # Detailed documentation
├── SETUP.md                                 # Setup and installation guide
└── QUICK_REFERENCE.md                       # This file
```

## 🎯 Components

### 1. **AccommodationViewPanel**
Main form with white background containing:
- Guest information (name, gender, contact)
- Date selection (check-in/out using spinners)
- Number of people selector
- Room type choice (VIP/Regular)
- Payment method integration
- Price calculation
- Book/Cancel buttons

### 2. **PaymentPanel**
Three payment options with dynamic fields:
- **mPesa**: Phone number entry
- **Debit Card**: Card details (number, name, expiry, CVV)
- **Credit Card**: Card details (number, name, expiry, CVV)

### 3. **FamilyPicturesPanel**
Gallery displaying 6 images in 3x2 grid:
- 3 room/hotel images
- 3 family/guest images
- Shows placeholders if images missing

### 4. **AccommodationDatabaseHelper**
Database helper methods:
- `saveBooking()` - Save new booking
- `getGuestBookings()` - Retrieve past bookings
- `cancelBooking()` - Cancel existing booking
- `isRoomAvailable()` - Check availability

## 🚀 Quick Start

### 1. **Access the Page**
```
Home Page → Click "Accommodation" button
OR
Sidebar → Click "Accommodation" link
```

### 2. **Fill the Form**
- [ ] Enter guest name
- [ ] Select gender
- [ ] Enter contact number
- [ ] Select check-in date (MM/DD/YYYY)
- [ ] Select check-out date (MM/DD/YYYY)
- [ ] Choose number of people (1-10)
- [ ] Select room type (VIP or Regular)
- [ ] Choose payment method
- [ ] Enter payment details

### 3. **Complete Booking**
- Click "Book Now" → Confirmation dialog appears
- Click "Cancel" → Form resets

## 💾 Database Integration

### Tables Used
- `hotel_rooms` - Room information
- `hotel_bookings` - Booking records

### Key Fields
- `guest_name` - Guest's name
- `guest_contact` - Phone number
- `room_id` - Foreign key to hotel_rooms
- `check_in_date` - Check-in date
- `check_out_date` - Check-out date
- `total_amount` - Total price
- `status` - Booking status (Booked/Cancelled)

## 💰 Pricing

| Room Type | Price per Night |
|-----------|-----------------|
| VIP       | ₦15,000        |
| Regular   | ₦8,000         |

## 🎨 Colors & Theme

Uses MELG Hotel theme:
- **Dark Green**: Dark backgrounds - #1B362D
- **Panel Green**: Panel backgrounds - #224838
- **Gold**: Text color - #E5DAC3
- **White**: Form background

## 📸 Image Locations

Required image files in `src/melg/hotel/images/`:
```
room1.jpg        - Room view 1
room2.jpg        - Room view 2
room3.jpg        - Room view 3
family1.jpg      - Family/guest picture 1
family2.jpg      - Family/guest picture 2
family3.jpg      - Family/guest picture 3
```

## 🔧 Configuration

### Change Prices
Edit in `AccommodationViewPanel.java`:
```java
vipRadio = new JRadioButton("VIP (₦15,000/night)");
regularRadio = new JRadioButton("Regular (₦8,000/night)");
```

### Change Currency
Replace "₦" symbol with:
- $ = Dollar
- € = Euro
- £ = Pound
- ₹ = Rupee

### Modify Date Range
In `createDatePanel()` method:
```java
new SpinnerNumberModel(currentYear, 2024, 2040, 1)
```
Change 2024 and 2040 to your desired year range.

## 📝 Usage Examples

### Save a Booking
```java
AccommodationDatabaseHelper.saveBooking(
    "John Doe",           // guest name
    "0712345678",         // contact
    "Male",               // gender
    4,                    // people count
    "2026-03-10",         // check-in
    "2026-03-12",         // check-out
    "VIP",                // room type
    "mPesa",              // payment method
    45000.00              // total amount
);
```

### Check Availability
```java
boolean available = AccommodationDatabaseHelper.isRoomAvailable(
    "Regular",
    "2026-03-10",
    "2026-03-12"
);
```

### Get Guest Bookings
```java
List<Map<String, String>> bookings = 
    AccommodationDatabaseHelper.getGuestBookings("John Doe");
```

### Cancel Booking
```java
AccommodationDatabaseHelper.cancelBooking(5); // booking ID 5
```

## ⚠️ Common Issues & Solutions

**Issue**: Images not showing
- **Solution**: Place image files in `src/melg/hotel/images/`

**Issue**: Module not appearing
- **Solution**: Ensure all java files compiled successfully

**Issue**: Database errors
- **Solution**: 
  1. Check MySQL/XAMPP is running
  2. Verify database name is "melgHotel"
  3. Check credentials in DatabaseHelper

**Issue**: Date picker issues
- **Solution**: Uses spinner components (no external library needed)

## 🔌 Integration Points

### From MELGHOTEL.java
```java
import melg.hotel.accommodation.AccommodationViewPanel;

// In AccommodationView wrapper class:
add(new AccommodationViewPanel(), BorderLayout.CENTER);
```

### From WelcomeView
```java
buttonPanel.add(createActionButton("Accommodation", "AccommodationView"));
```

### From SidebarPanel
```java
addButton(linksPanel, "Accommodation", "AccommodationView");
```

## 📱 Responsive Design

The accommodation module:
- ✅ Scrolls on small screens
- ✅ Adapts form width responsively
- ✅ Works on standard desktop (1200x800+)
- ✅ Images scale automatically

## 🔐 Security Considerations

For production use:
- Hash payment card data
- Use HTTPS for data transmission
- Implement input validation
- Add transaction logging
- Sanitize SQL queries (currently uses PreparedStatements ✓)

## 📚 Related Files

- Main app: `src/melg/hotel/MELGHOTEL.java`
- Welcome view: Referenced in Application
- Database helper: `DatabaseHelper` inner class in MELGHOTEL.java
- Theme colors: `Theme` inner class in MELGHOTEL.java

## 🎓 Learning Path

1. Start with `README.md` for overview
2. Read `SETUP.md` for installation
3. Review `AccommodationViewPanel.java` for UI
4. Study `AccommodationDatabaseHelper.java` for database ops
5. Check MELGHOTEL.java for integration

## 📞 Support

For issues or questions:
1. Check the relevant documentation file
2. Review inline code comments
3. Check SETUP.md troubleshooting section
4. Verify all files are in correct locations

---

**Version**: 1.0  
**Last Updated**: March 2026  
**Status**: Complete and Ready for Use
