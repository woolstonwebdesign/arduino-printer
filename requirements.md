# Requirements and Specifications for Arduino Printer
## Table of Contents
* [Project Description](#project-description)
* [Device Specifications](#device-specifications)
  * [Arduino](#arduino)
  * [Printer](#printer)
* [Data Workflow](#data-workflow)

## Project Description
This project will create a device which is made up of two components
* arduino-styled device
* thermal printer

These two devices together will operate as a bench-top printing solution for merchants who have an online store. These merchants will generally be in the business of producing goods quickly where an order is given and the product is required as quickly as possible while the buyer either waits for the product, arrives in-store to pickup the product or the product is delivered to them.

The content printed is not relevent to the project because the arduino device will connect to a specific page on the merchant's online store and simply render whatever content is shown on that page. That way, the printer does not need to interpret anything and the arduino simply passes ascii text to the printer. All formatting etc will be done on the merchant's online store page.

## Device Specifications
### Arduino
This device must allow the following functionality:
* internet connectivity via ethernet and/or wifi
* allow a user to customise the destination URL that it will hit
* allow a user to customise the interval of time between URL polls. For example, some merchants may want to check for orders every 3 minutes where others may only require 30 minute checks
* hit the destination URL repeatedly using the configurable interval. This interval should be a positive integer indicating the interval in minutes

### Printer
This device should be a thermal printer so that there are minimal replacement parts.

The printer should accept print requests from the arduino and simply print any ascii text that is send to it. The length of this content is unknown because orders could have large numbers of items, so the printer should be able to accept large amounts of data. This could be limited to 300 lines of text if an upper limit is required.

## Data Workflow
This is a linear example of how content will pass in and out of the devices.

1. An order is placed on the merchant's online store. The store will be responsible for making that order data available at a specific URL/endpoint in a formatted fashion
2. The arduino polls that URL/endpoint every n minutes. The arduino will look for some kind of identifying feature either in the URL content or request header to indicate that there is content ready to be printed
3. The arduino detects there is content to be printed and passes the content as a print request to the thermal printer
4. The online store will update itself to indicate that the order(s) has been sent to the arduino. When this occurs, that order(s) will be updated so as to not appear in the next arduino poll
5. The printer prints out the content