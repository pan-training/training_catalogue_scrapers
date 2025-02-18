# PaN Training Catalogue Scrapers

## About

These are a collection of Ruby scripts designed to scrape web pages (or other useful resources) and create Events or Materials on the [PaN catalogue](https://pan-training.hzdr.de). They require the PaN Catalogue or TeSS API client
in order to function: https://github.com/pan-training/training-catalogue-api-client.

## Running


Install all dependencies by running this command in the root directory:

`bundle install`

From the root directory copy the example_uploader_config.txt into uploader_config.txt with the command:

`cp example_uploader_config.txt uploader_config.txt`

and configure appropriately to your TeSS instance.

You have an *authentication token* generated by TeSS when you sign up for an account. Go to your profile page on TeSS and copy the secret token into the user_token field in uploader_config.txt.

To generate a Google API key for finding the geolocation of addresses you will [need to register for a free key here](https://developers.google.com/maps/documentation/javascript/get-api-key)

To run all scrapers:

`bundle exec ruby run_scrapers.rb`

This runs all scrapers listed in the run_scrapers.rb file.

To run an individual scraper run *run.rb* with the name of a scraper class from the app/scrapers/ folder. For example:

`bundle exec ruby run.rb LightsourcesEventScraper`

## Writing scrapers

Scrapers are very varied. Some sites TeSS aggregates require HTML parsing techniques such as with Nokogiri to extract metadata about, some are formatted in schema.org and can be extracted using RDF gems, and some are XML or JSON documents that need to be parsed and processed before being uploaded to TeSS.

In TeSS, scraper classes (despite different approaches to parsing) have similar structures. Each inherit from the TeSS::Scrapers::Scraper module, they implement the method *scrape()*, they perform their various functions to extract information from the source site; then proceed to create an Event, Material, or ContentProvider object. They use the methods *add_material()*, *add_event()*, and *add_content_provider()* to push these objects to the configured upstream TeSS instance.

You can see lots of examples of how to implement a new scraper class in app/scrapers/ folder. The module TeSS::SCrapers::Scrapepr can be found lib/tess/scrapers/scraper.rb where you can see all the available functions and methods.




