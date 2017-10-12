# android-phonefield-Input

android-phone-field is A small UI library that allows you to create phone fields with corresponding country flags, and validate the phone number using libphonenumber from google.


<img src="https://raw.githubusercontent.com/lamudi-gmbh/android-phone-field/master/raw/phone-field.gif" alt="alt text" title="Sample App" style="max-width:100%;">

#The library has two different fields:

# PhoneEditText : 

includes EditText alongside the flags spinner
#PhoneInputLayout : 
includes a TextInputLayout from the design support library alongside the flags spinner

# Features

Displays the correct country flag if the user enters a valid international phone number
Allows the user to choose the country manually and only enter a national phone number
Allows you to choose a default country, which the field will change to automatically if the user chose a different country then cleared the field.

#Validates the phone number
Returns the valid phone number including the country code


# Usage

# 1. Add this library project as module in Android Studio.
-So your app will be having module dependancy of this Lib.

Now lets get started:

# 2.In your layout you can use the PhoneInputLayout
<code>
<com.lamudi.phonefield.PhoneInputLayout
     android:id="@+id/phone_input_layout"
     android:layout_width="match_parent"
     android:layout_height="wrap_content"/>
     
 </code>    
or the PhoneEditText

<code>

 <com.lamudi.phonefield.PhoneEditText
     android:id="@+id/edit_text"
     android:layout_width="match_parent"
     android:layout_height="wrap_content"/>
     
     </code>
#3.Then in your Activity/Fragment

<code>
final PhoneInputLayout phoneInputLayout = (PhoneInputLayout) findViewById(R.id.phone_input_layout);
final PhoneEditText phoneEditText = (PhoneEditText) findViewById(R.id.edit_text);
final Button button = (Button) findViewById(R.id.submit_button);

// you can set the hint as follows
phoneInputLayout.setHint(R.string.phone_hint);
phoneEditText.setHint(R.string.phone_hint);

// you can set the default country as follows
phoneInputLayout.setDefaultCountry("DE");
phoneEditText.setDefaultCountry("FR");

button.setOnClickListener(new View.OnClickListener() {
  @Override
  public void onClick(View v) {
    boolean valid = true;
    
    // checks if the field is valid 
    if (phoneInputLayout.isValid()) {
      phoneInputLayout.setError(null);
    } else {
      // set error message
      phoneInputLayout.setError(getString(R.string.invalid_phone_number));
      valid = false;
    }

    if (phoneEditText.isValid()) {
      phoneEditText.setError(null);
    } else {
      phoneEditText.setError(getString(R.string.invalid_phone_number));
      valid = false;
    }

    if (valid) {
      Toast.makeText(MainActivity.this, R.string.valid_phone_number, Toast.LENGTH_LONG).show();
    } else {
      Toast.makeText(MainActivity.this, R.string.invalid_phone_number, Toast.LENGTH_LONG).show();
    }
    
    // Return the phone number as follows
    String phoneNumber = phoneInputLayout.getPhoneNumber();
  }
});


</code>
 
# Customization

In case the default style doesn't match your app styles, you can extend the PhoneInputLayout, or PhoneEditText and provide your own xml, but keep in mind that you have to provide a valid xml file with at least an EditText (tag = com_lamudi_phonefield_edittext) and Spinner (tag = com_lamudi_phonefield_flag_spinner), otherwise the library will throw an IllegalStateException.

You can also create your own custom view by extending the PhoneField directly.

# Countries generation

For better performance and to avoid using json data and then parse it to be used in the library, a simple nodejs is used to convert the countries.json file in raw/countries-generator/ into a plain java utility class that has static list of countries.

The generation script works as follows:

node gen.js

or

./gen.js

# Motivation

This is probably not the the first library with the same purpose, for instance before I started working on the library I came across IntlPhoneInput which provides almost most of the functionality this library provides, however I chose to develop a new library for the following reasons:

This library provides two implementations of PhoneField using EditText and TextInputLayout
This library allows users to extend the functionality and use custom layouts if needed to match the application theme
This library uses a static list of countries generated from the countries.json file in the raw resources

# Attributions

Inspired by intl-tel-input for jQuery and IntlPhoneInput
Flag images from flags
Original country data from mledoze's World countries in JSON, CSV and XML which is then used to generate a plain Java file
Formatting/validation using libphonenumber

# Note:
If you find newly issued mobile numbers not validated as mobile number for any country you can add supporting them by using latest dependancy of 

<code> compile 'com.googlecode.libphonenumber:libphonenumber:X.X.X'  </code></br></br>
in your android-phonefield-Input gradle.
So that this library will support latest issued numbers.

# Example senario:
For library whis is using com.googlecode.libphonenumber:libphonenumber:7.X.X  versions ,
JIO numbers starting with 89XXX XXXXX was not a mobile number in India.

but when i migrated to com.googlecode.libphonenumber:libphonenumber:8.X.X  support was there.

You can check latest <a href="https://github.com/googlei18n/libphonenumber">Here</a>

# If you liked this Project, Please <a href="https://github.com/googlei18n/libphonenumber">Follow me</a>...

