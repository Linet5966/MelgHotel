# Accommodation Module Setup Guide

## Prerequisites

### Required Libraries
The Accommodation module uses the following library for date selection:
- **JCalendar** - For JDateChooser component

### Add JCalendar to Your Project

1. **Download JCalendar**
   - Download from: https://www.toedter.com/en/jcalendar/
   - Or use Maven: Add to pom.xml if using Maven

2. **Add JAR to Classpath**
   - In NetBeans IDE:
     - Right-click on project → Properties
     - Go to Libraries section
     - Add JAR/Folder
     - Select `jcalendar-1.4.jar` (or latest version)

3. **Maven Setup** (if applicable)
   ```xml
   <dependency>
       <groupId>com.toedter</groupId>
       <artifactId>jcalendar</artifactId>
       <version>1.4</version>
   </dependency>
   ```

## Image Setup

### Directory Structure
Create the following directory if it doesn't exist:
```
src/
  melg/
    hotel/
      images/
        (place image files here)
```

### Required Image Files

Place the following images in `src/melg/hotel/images/`:

#### Room Images (3 required)
- `room1.jpg` - Main bedroom view
- `room2.jpg` - Bathroom or suite area
- `room3.jpg` - Hotel common area or exterior

#### Family Pictures (3 required)
- `family1.jpg` - Guest/family gathering
- `family2.jpg` - Hotel event or dining
- `family3.jpg` - Outdoor/recreational area

### Image Specifications
- **Format**: JPG, PNG, or GIF
- **Recommended Size**: At least 500x400 pixels
- **Aspect Ratio**: 4:3 or 16:10 for best fit

### Using Placeholder Images (if real images unavailable)

If images are not available, the system will display placeholder text labels:
```
[Image: room1.jpg]
[Image: family1.jpg]
etc.
```

## Compilation & Build

### NetBeans IDE
1. Clean and Build Project:
   - Right-click Project → Clean and Build
   
2. Run the Application:
   - Right-click → Run
   - Navigate to Accommodation page

### Command Line (Maven)
```bash
mvn clean compile
mvn exec:java -Dexec.mainClass="melg.hotel.MELGHOTEL"
```

### Command Line (Gradle)
```bash
gradle clean build
gradle run
```

## Troubleshooting

### Error: `com.toedter.calendar.JDateChooser cannot be found`
**Solution**: Add JCalendar library to project classpath (see Prerequisites section)

### Error: Image files not loading
**Solution**: 
1. Verify image files are in `src/melg/hotel/images/`
2. Check file names match exactly (case-sensitive on Linux/Mac)
3. Use absolute paths if resources folder is not in classpath

### Form not appearing
**Solution**:
1. Check that AccommodationViewPanel class compiled successfully
2. Verify PaymentPanel and FamilyPicturesPanel are in the same package
3. Check imports in MELGHOTEL.java

## Testing the Module

1. **Launch Application**
   - Run MELGHOTEL.java main method

2. **Navigate to Accommodation**
   - Click "Accommodation" in sidebar OR
   - Click "Accommodation" button on home page

3. **Test Features**
   - Enter guest information
   - Select dates using calendar
   - Choose room type (VIP/Regular)
   - Select payment method
   - Click "Book Now" to confirm (displays confirmation dialog)
   - Click "Cancel" to reset form

## File Organization

```
MELG-HOTEL/
  src/
    melg/
      hotel/
        accommodation/
          ├── AccommodationViewPanel.java
          ├── PaymentPanel.java
          ├── FamilyPicturesPanel.java
          ├── README.md
          └── SETUP.md (this file)
        images/
          ├── room1.jpg
          ├── room2.jpg
          ├── room3.jpg
          ├── family1.jpg
          ├── family2.jpg
          └── family3.jpg
        MELGHOTEL.java
```

## Customization

### Change Room Prices
Edit in `AccommodationViewPanel.java`:
```java
vipRadio = new JRadioButton("VIP (₦15,000/night)", false);
regularRadio = new JRadioButton("Regular (₦8,000/night)", true);
```

### Change Currency Symbol
Search for "₦" in accommodationviewpanel.java and replace with your currency symbol:
- $ for Dollar
- € for Euro
- £ for Pound
- ₹ for Rupee

### Modify Form Fields
All form fields are created in the `createFormPanel()` method. Add new fields by:
1. Creating component (JTextField, JComboBox, etc.)
2. Adding to GridBagLayout with appropriate constraints
3. Making it an instance variable if needed elsewhere

## Database Integration

The booking form data should be saved to the existing database:

```sql
INSERT INTO hotel_bookings 
(guest_name, guest_contact, room_id, check_in_date, check_out_date, total_amount, status)
VALUES (?, ?, ?, ?, ?, ?, 'Booked');
```

Enhanced button click handlers should include database insertion logic.

## Support & Documentation

For detailed information about each component:
- See `README.md` in the accommodation folder
- Check inline code comments
- Review MELGHOTEL.java main class for theme and styling

---
**Last Updated**: March 2026
**Module Version**: 1.0
