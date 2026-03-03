# MELG Hotel - Accommodation Module

## Overview
The Accommodation module provides a complete booking system for hotel guests. It includes guest information collection, room type selection, and multiple payment options.

## Module Files

### **AccommodationViewPanel.java**
Main accommodation booking form panel that includes:
- Guest name and contact information
- Gender selection dropdown
- Check-in and check-out date pickers
- Number of people selection
- Room type selection (VIP or Regular)
- Total price calculation
- Book/Cancel buttons

**Features:**
- White form background for optimal readability
- Integrated with PaymentPanel for payment method selection
- Displays FamilyPicturesPanel showing hotel and family images
- Real-time room pricing updates based on room type

### **PaymentPanel.java**
Payment method selection panel with three options:

1. **mPesa**
   - Phone number field
   - Automatic prompt system

2. **Debit Card**
   - Card number
   - Cardholder name
   - Expiry date
   - CVV

3. **Credit Card**
   - Card number
   - Cardholder name
   - Expiry date
   - CVV

**Features:**
- Dynamic field visibility (shows/hides based on selection)
- Clean, organized panel layout
- Styled with hotel theme colors

### **FamilyPicturesPanel.java**
Gallery panel displaying hotel and family images in a 3-column grid layout.

**Features:**
- 6-image display grid (3x2)
- Automatic image scaling
- Placeholder display if images are not found
- Responsive design with proper spacing

## Room Types & Pricing

- **VIP Room**: ₦15,000 per night
- **Regular Room**: ₦8,000 per night

## Integration

The accommodation module is fully integrated into the main MELGHOTEL application:
- Accessible from the sidebar navigation
- Accessible from the Welcome page "Accommodation" button
- Uses the existing Theme system for consistent styling
- Implements NavigationListener for page navigation

## Image Resources Required

To display images, place the following files in `src/melg/hotel/images/`:
- `room1.jpg` - Hotel room image 1
- `room2.jpg` - Hotel room image 2
- `room3.jpg` - Hotel room image 3
- `family1.jpg` - Family/guest image 1
- `family2.jpg` - Family/guest image 2
- `family3.jpg` - Family/guest image 3

If images are not found, placeholder labels will be displayed.

## Form Fields

### Guest Information
- **Guest Name** (text field)
- **Gender** (dropdown: Male, Female, Other)
- **Contact Number** (text field)

### Booking Details
- **Check-in Date** (date picker)
- **Check-out Date** (date picker)
- **Number of People** (spinner: 1-10)
- **Room Type** (radio buttons: VIP or Regular)

### Payment
- **Payment Method** (radio buttons: mPesa, Debit Card, or Credit Card)
- Relevant payment details based on selected method

## Color Scheme

The module uses the established MELG Hotel theme:
- **Dark Green Background**: #1B362D
- **Panel Green**: #224838
- **Gold Text**: #E5DAC3
- **White**: #FFFFFF (form background)

## Usage

To book a room:
1. Navigate to the "Accommodation" page from the sidebar or home page
2. View the family/hotel pictures gallery
3. Fill in personal information (name, gender, contact)
4. Select check-in and check-out dates
5. Specify number of people
6. Choose between VIP or Regular room
7. Select preferred payment method and enter payment details
8. Click "Book Now" to confirm booking

Click "Cancel" to reset the form and start over.

## Database Integration

The form collects data that integrates with the existing MELGHOTEL database:
- Guest information stores in `hotel_bookings` table
- Room details are tracked in `hotel_rooms` table
- Booking status is maintained as "Booked"

## Future Enhancements

- Room availability calendar
- Real-time pricing based on demand
- Loyalty program integration
- Email confirmation system
- SMS payment notifications
- Photo upload for guest profiles
