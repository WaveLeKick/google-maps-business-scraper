[Google Maps Business Scraper](https://apify.com/lazymac/google-maps-business-scraper?fpr=data)

# Google Maps Business Scraper

Extract comprehensive business data from Google Maps at scale. Get business names, addresses, phone numbers, websites, ratings, reviews, opening hours, coordinates, photos, and 20+ data fields for any search query or location.

Built for **sales teams, marketing agencies, lead generation specialists, market researchers**, and anyone who needs structured local business data from Google Maps.

## Why use this scraper?

Google Maps is the world's largest local business directory, with data on over 200 million businesses across every country. This actor lets you extract that data in structured, machine-readable format ready for your CRM, spreadsheet, or data pipeline.

**Key advantages:**

- **Comprehensive data** — 25+ fields per business including contact info, ratings, coordinates, and opening hours
- **Smart filtering** — Filter by rating, review count, phone availability, and website presence
- **Multi-query support** — Search for multiple queries or locations in a single run
- **Review extraction** — Get individual review text, ratings, and author data
- **Photo URLs** — Extract business photos for visual verification
- **Proxy rotation** — Built-in residential proxy support to avoid rate limiting
- **Pay-per-event pricing** — Only pay for results you actually get

## What data can you extract?

Every business listing includes up to 25+ structured fields:

| Field | Description | Example |
| --- | --- | --- |
| `title` | Business name | "Joe's Pizza" |
| `categoryName` | Business category | "Pizza Restaurant" |
| `address` | Full street address | "123 Main St, New York, NY 10001" |
| `street` | Street address component | "123 Main St" |
| `city` | City name | "New York" |
| `state` | State/province code | "NY" |
| `postalCode` | ZIP/postal code | "10001" |
| `countryCode` | Country code | "US" |
| `phone` | Phone number | "+1 (212) 555-0123" |
| `website` | Business website URL | "[https://joespizza.com](https://joespizza.com)" |
| `url` | Google Maps URL | "[https://google.com/maps/place/](https://google.com/maps/place/)..." |
| `totalScore` | Average rating (1-5) | 4.5 |
| `reviewsCount` | Total number of reviews | 342 |
| `priceLevel` | Price range indicator | "$$" |
| `latitude` | GPS latitude | 40.7128 |
| `longitude` | GPS longitude | -74.0060 |
| `placeId` | Google Place ID | "ChIJN1t_tDeuEmsRUsoyG83frY4" |
| `cid` | Google Maps CID | "12345678901234567" |
| `status` | Business status | "OPERATIONAL" |
| `description` | Business description | "Family-owned since 1975..." |
| `imageUrl` | Main business image URL | "[https://lh5.googleusercontent.com/](https://lh5.googleusercontent.com/)..." |
| `permanentlyClosed` | Is permanently closed? | false |
| `temporarilyClosed` | Is temporarily closed? | false |
| `openingHours` | Weekly opening hours | [{day: "Monday", hours: "9 AM - 5 PM"}] |
| `reviews` | Individual review data | [{author, rating, text, date}] |
| `photos` | Photo URLs | ["[https://...jpg](https://...jpg)", ...] |
| `additionalInfo` | Amenities, attributes | {wheelchair: true, wifi: true} |
| `scrapedAt` | Timestamp of extraction | "2026-04-16T12:00:00.000Z" |
| `searchQuery` | Original search query | "restaurants in New York" |

## Use cases

### Lead Generation for Sales Teams

Extract business contact information (phone numbers, websites, addresses) for targeted outreach campaigns. Filter by rating and review count to focus on established businesses.

```
Search: "dentists in Chicago IL"
Filter: Rating >= 4.0, Has Phone, Has Website
Result: 50 qualified dental practice leads with contact info
```

### Market Research & Competitive Analysis

Analyze the competitive landscape in any market by extracting all businesses in a category within a geographic area. Compare ratings, review counts, and pricing.

```
Search: "coffee shops in Seattle"
Include: Reviews, Opening Hours, Additional Info
Result: Complete competitive analysis dataset
```

### Real Estate & Location Intelligence

Map all businesses around a specific address or neighborhood. Understand the commercial density, types of businesses, and walkability scores.

```
Search: "businesses near Times Square New York"
Include: Coordinates, Opening Hours
Result: Geospatial business density data
```

### Franchise & Expansion Planning

Find areas with high demand but low supply for a specific business type. Identify underserved markets for expansion opportunities.

```
Search: "pizza restaurants in Austin TX"
Compare against: "pizza restaurants in Dallas TX"
Result: Market gap analysis between cities
```

### Review Monitoring & Reputation Management

Track reviews for businesses in your portfolio or industry. Monitor competitor sentiment and identify trends.

```
Search: "your business name city"
Include: Reviews (max 50), Sort by Newest
Result: Latest customer sentiment data
```

### Directory & Listing Verification

Verify that business information on your website or directory matches Google Maps data. Identify outdated phone numbers, addresses, or closed businesses.

## Input configuration

### Search Configuration

#### Search Queries

The primary way to find businesses. Enter one or more search queries, each on a new line. For best results, include the location in your query.

**Examples:**

- `restaurants in San Francisco` — Find all restaurants in SF
- `plumber near 90210` — Find plumbers near a ZIP code
- `hotels in Paris France` — International search
- `car repair shop downtown Denver` — Neighborhood-level search
- `vegan restaurant Manhattan NYC` — Specific cuisine + area

#### Start URLs

For advanced users who already have Google Maps URLs. You can provide:

- **Search result URLs**: `https://www.google.com/maps/search/restaurants+in+chicago/`
- **Individual place URLs**: `https://www.google.com/maps/place/Joe's+Pizza/...`

### Maximum Results

Control how many results to extract per query. Google Maps typically shows 20-120 results depending on the search. Set to 0 for unlimited.

**Recommended settings:**

- Quick sample: 10-20 results
- Standard search: 50 results (default)
- Comprehensive: 100-200 results
- Full extraction: 0 (unlimited)

### Localization

#### Language

Set the language for business names, addresses, and descriptions. Uses ISO 639-1 codes:

- `en` — English (default)
- `es` — Spanish
- `fr` — French
- `de` — German
- `ja` — Japanese
- `ko` — Korean
- `zh` — Chinese
- `pt` — Portuguese
- `ar` — Arabic
- `hi` — Hindi

#### Country Code

Two-letter ISO country code to target the correct Google Maps regional domain:

- `US` — United States (default)
- `GB` — United Kingdom
- `CA` — Canada
- `AU` — Australia
- `DE` — Germany
- `FR` — France
- `JP` — Japan
- `KR` — South Korea
- `BR` — Brazil
- `IN` — India

### Data Extraction Options

#### Include Reviews

When enabled, extracts individual reviews including:

- Reviewer name
- Star rating (1-5)
- Review text
- Review date

**Note:** Enabling reviews significantly increases run time as it requires loading additional data for each business.

#### Review Sort Order

Control which reviews are extracted first:

- **Most Relevant** — Google's default ranking (recommended)
- **Newest First** — Most recent reviews
- **Highest Rating** — 5-star reviews first
- **Lowest Rating** — 1-star reviews first (useful for reputation monitoring)

#### Include Photos

Extract URLs for business photos. Useful for:

- Visual verification of businesses
- Building rich listing pages
- Image-based analysis

#### Include Opening Hours

Get structured weekly opening hours for each business. Returns an array with day name and time range for each day of the week.

#### Include Additional Info

Extract business attributes and amenities like:

- Wheelchair accessibility
- Wi-Fi availability
- Outdoor seating
- Payment methods accepted
- Dining options (dine-in, takeout, delivery)
- Parking availability

### Filters

#### Minimum Rating Filter

Only include businesses rated at or above this value (0-5). Examples:

- `0` — Include all businesses (default)
- `3.5` — Exclude poorly-rated businesses
- `4.0` — Only well-rated businesses
- `4.5` — Only top-rated businesses

#### Minimum Reviews Count

Only include businesses with at least this many reviews. Useful for filtering out new or inactive businesses:

- `0` — Include all (default)
- `10` — Has some reviews
- `50` — Established business
- `100` — Well-known business

#### Only With Phone Number

When enabled, skips businesses without a listed phone number. Essential for:

- Cold calling campaigns
- Telemarketing outreach
- Phone verification workflows

#### Only With Website

When enabled, skips businesses without a website. Essential for:

- Digital marketing campaigns
- Website audit services
- Online advertising outreach

### Performance

#### Max Concurrency

Number of pages to process simultaneously. Higher values = faster scraping but higher risk of rate limiting.

- `1-3` — Safe, slow
- `5` — Balanced (default)
- `10-20` — Fast, may trigger blocks

#### Proxy Configuration

Configure proxy settings for reliable scraping. **Residential proxies are strongly recommended** for Google Maps to avoid blocks.

Default: Apify residential proxy group (`RESIDENTIAL`)

## Output example

### Single business result (JSON)

```
{
    "title": "Golden Gate Pizza & Pasta",
    "categoryName": "Italian Restaurant",
    "address": "542 Clement St, San Francisco, CA 94118",
    "street": "542 Clement St",
    "city": "San Francisco",
    "state": "CA",
    "postalCode": "94118",
    "countryCode": "US",
    "phone": "+1 (415) 555-0142",
    "website": "https://goldengatepizza.com",
    "url": "https://www.google.com/maps/place/Golden+Gate+Pizza/...",
    "totalScore": 4.6,
    "reviewsCount": 892,
    "priceLevel": "$$",
    "latitude": 37.7829,
    "longitude": -122.4694,
    "placeId": "ChIJd7zN_thfj4AR_06S9VV15FY",
    "status": "OPERATIONAL",
    "permanentlyClosed": false,
    "temporarilyClosed": false,
    "description": "Casual Italian spot with classic pizzas and pasta dishes since 1985.",
    "imageUrl": "https://lh5.googleusercontent.com/p/AF1QipN...",
    "openingHours": [
        { "day": "Monday", "hours": "11:00 AM - 10:00 PM" },
        { "day": "Tuesday", "hours": "11:00 AM - 10:00 PM" },
        { "day": "Wednesday", "hours": "11:00 AM - 10:00 PM" },
        { "day": "Thursday", "hours": "11:00 AM - 10:00 PM" },
        { "day": "Friday", "hours": "11:00 AM - 11:00 PM" },
        { "day": "Saturday", "hours": "11:00 AM - 11:00 PM" },
        { "day": "Sunday", "hours": "12:00 PM - 9:00 PM" }
    ],
    "scrapedAt": "2026-04-16T12:34:56.789Z",
    "searchQuery": "restaurants in San Francisco"
}
```

### With reviews enabled

```
{
    "title": "Golden Gate Pizza & Pasta",
    "totalScore": 4.6,
    "reviewsCount": 892,
    "reviews": [
        {
            "author": "Sarah M.",
            "rating": 5,
            "text": "Best pizza in the Richmond district! The margherita is incredible and the pasta is always perfectly al dente. Great family atmosphere.",
            "date": "2026-03-15"
        },
        {
            "author": "James K.",
            "rating": 4,
            "text": "Solid neighborhood spot. Good food, reasonable prices. Can get crowded on weekends.",
            "date": "2026-03-10"
        }
    ]
}
```

## Integration examples

### Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")

run_input = {
    "searchQueries": [
        "dentists in Chicago IL",
        "dentists in Houston TX",
    ],
    "maxResults": 100,
    "language": "en",
    "countryCode": "US",
    "includeReviews": False,
    "includeOpeningHours": True,
    "filterByRating": 4.0,
    "onlyWithPhone": True,
    "onlyWithWebsite": True,
}

run = client.actor("lazymac2x/google-maps-business-scraper").call(run_input=run_input)

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item['title']} | {item['phone']} | {item['website']}")
```

### Node.js

```
const { ApifyClient } = require('apify-client');

const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const input = {
    searchQueries: ['plumbers in Los Angeles CA'],
    maxResults: 50,
    includeOpeningHours: true,
    onlyWithPhone: true,
};

(async () => {
    const run = await client.actor('lazymac2x/google-maps-business-scraper').call(input);
    const { items } = await client.dataset(run.defaultDatasetId).listItems();

    items.forEach(item => {
        console.log(`${item.title} - ${item.phone} - ${item.totalScore} stars`);
    });
})();
```

### API (cURL)

```
# Start the actor
curl -X POST "https://api.apify.com/v2/acts/lazymac2x~google-maps-business-scraper/runs" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "searchQueries": ["restaurants in Miami FL"],
    "maxResults": 50,
    "includeOpeningHours": true,
    "onlyWithPhone": true
  }'

# Get results (use the datasetId from the run response)
curl "https://api.apify.com/v2/datasets/DATASET_ID/items?format=json" \
  -H "Authorization: Bearer YOUR_API_TOKEN"
```

### Zapier Integration

This actor works seamlessly with Zapier through the official Apify integration:

1. **Add the Apify trigger** in Zapier (or use the "Run Actor" action)
2. **Set the actor** to `lazymac2x/google-maps-business-scraper`
3. **Configure input** with your search queries and filters
4. **Connect to your CRM** — automatically push leads to HubSpot, Salesforce, or Pipedrive
5. **Schedule runs** — set up daily/weekly scraping for fresh leads

### Google Sheets Export

Export results directly to Google Sheets:

1. Run the actor with your desired input
2. Go to the dataset results page
3. Click "Export" and choose "Google Sheets"
4. Or use the Apify API to programmatically push data to Sheets

### CSV/Excel Export

All results can be exported in CSV, JSON, XML, Excel, or HTML format:

```
# Export as CSV
curl "https://api.apify.com/v2/datasets/DATASET_ID/items?format=csv" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -o businesses.csv

# Export as Excel
curl "https://api.apify.com/v2/datasets/DATASET_ID/items?format=xlsx" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -o businesses.xlsx
```

## Tips for best results

### Optimizing search queries

- **Be specific with location**: "pizza in Brooklyn NY" works better than "pizza in New York"
- **Use business categories**: "Italian restaurant" finds more results than just "restaurant"
- **Add neighborhoods**: "barber shop Williamsburg Brooklyn" narrows results effectively
- **Try ZIP codes**: "gym near 90210" targets a specific area
- **Combine with qualifiers**: "best rated plumber in Dallas TX" targets top results

### Controlling costs

- Start with a small `maxResults` (10-20) to test your query
- Disable reviews and photos if you only need contact info
- Use filters (rating, phone, website) to reduce output size
- Set appropriate `maxConcurrency` (default 5 is good for most cases)

### Avoiding blocks

- Use residential proxies (default configuration)
- Keep `maxConcurrency` at 5 or below for large runs
- Avoid running too many queries simultaneously
- Space out large runs (1000+ results) over time

### Getting the most data

- Enable `includeReviews` for sentiment analysis
- Enable `includePhotos` for visual verification
- Enable `includeAdditionalInfo` for amenity data
- Set `includeOpeningHours` to true (default) for availability data
- Use `maxReviews: 50` for detailed review analysis

## Pricing

This actor uses **Pay-Per-Event (PPE)** pricing:

- You are charged per result scraped
- No charge for failed or filtered-out results
- Check the actor's pricing page for current rates

**Cost estimation:**

- 50 businesses (basic data): ~$0.50
- 50 businesses (with reviews): ~$1.00
- 100 businesses (basic data): ~$1.00
- 500 businesses (basic data): ~$5.00

## Limitations

- **Google Maps rate limiting**: Google may limit results for very high-volume queries. Use residential proxies and moderate concurrency.
- **Review count**: Maximum ~100 reviews per business can be extracted. Google limits review visibility.
- **Real-time data**: Results reflect Google Maps data at the time of scraping. Business information changes over time.
- **Search result limits**: Google Maps shows a maximum of approximately 120 results per search query. For more results, use multiple overlapping queries with different location modifiers.
- **Coordinates accuracy**: Coordinates extracted from URLs may have reduced precision compared to the Google Places API.

## FAQ

### How many results can I get per search?

Google Maps typically shows 20-120 results per search query depending on the location and category density. For maximum coverage, use multiple specific queries (e.g., search by neighborhood instead of entire city).

### Can I scrape businesses worldwide?

Yes. Set the `countryCode` to target any country and `language` for localized results. The scraper works with all Google Maps regional domains.

### How fresh is the data?

Data is extracted in real-time from Google Maps. Each run gives you the most current information Google has for each business.

### Do I need proxies?

Residential proxies are strongly recommended and enabled by default. Without proxies, Google may block requests after a small number of queries.

### How do I get phone numbers for all businesses?

Enable the `onlyWithPhone` filter to only include businesses with listed phone numbers. Note that not all businesses on Google Maps have phone numbers listed.

### Can I search by geographic coordinates?

Yes. Use the `startUrls` input with a Google Maps URL that includes coordinates, such as: `https://www.google.com/maps/search/restaurants/@40.7128,-74.006,15z/`

### How do I extract reviews?

Set `includeReviews` to `true` and configure `maxReviews` (default 5). Reviews include author name, star rating, text content, and date.

### What format are the results in?

Results are stored in an Apify dataset and can be exported as JSON, CSV, XML, Excel, HTML, or RSS. You can also access results via the API.

### Can I schedule regular runs?

Yes. Use Apify's scheduling feature to run the scraper daily, weekly, or at any custom interval. Great for monitoring new businesses or tracking review changes.

### How do I filter out closed businesses?

The scraper includes `permanentlyClosed` and `temporarilyClosed` fields. You can filter these out in post-processing, or use the rating/review filters to focus on active businesses (closed businesses typically have no recent reviews).

### Can I use this for lead generation?

Absolutely. This is the primary use case. Combine search queries targeting your ideal customer profile with the `onlyWithPhone` and `onlyWithWebsite` filters to get qualified leads with contact information.

### Is this legal?

Web scraping of publicly available data is generally legal in most jurisdictions. Google Maps data is publicly visible to anyone. However, you should comply with Google's Terms of Service and your local regulations. This scraper is designed for research and legitimate business purposes.

### How does pricing work?

This actor uses Pay-Per-Event pricing. You are charged for each successfully scraped business result. Failed requests, filtered-out results, and search page loads are not charged. This means you only pay for actual data you receive.

### Can I connect this to my CRM?

Yes. Use the Apify API or Zapier integration to push results directly to HubSpot, Salesforce, Pipedrive, or any CRM with an API. You can also use webhook notifications to trigger workflows when a run completes.

## Changelog

### v1.0.0 (2026-04-16)

- Initial release
- Search by query or direct Google Maps URLs
- 25+ data fields per business
- Review extraction with sort options
- Photo URL extraction
- Opening hours extraction
- Rating, review count, phone, and website filters
- Multi-query support
- Residential proxy support
- Pay-per-event pricing
- Python, Node.js, cURL, and Zapier integration examples

## Support

If you encounter any issues or have feature requests:

- Open an issue on the actor's GitHub repository
- Contact us through Apify's messaging system
- Check the FAQ section above for common questions

## Related actors

- **Google Maps Reviews Scraper** — Focused on extracting reviews in depth
- **Google Search Scraper** — Scrape Google SERP results
- **Yellow Pages Scraper** — Alternative business directory
- **Yelp Scraper** — Reviews and business data from Yelp