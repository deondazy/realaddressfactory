# RealAddress Generator (Laravel 12 Fork)
## About
**Fork Notice**: This is a community-maintained fork of [nonsapiens/realaddressfactory](https://github.com/nonsapiens/realaddressfactory) with Laravel 12 support.

This library creates actual, 100% real addresses with full address details and lat/long coordinates using the Google Maps API. Features include:
- Laravel 12 compatibility
- Faker integration for database seeding
- Address generation via Facade or direct class usage

## Installation
Require this package with composer:
```bash
composer require deondazy/realaddressfactory --dev
```

### Google Maps API Requirements
Add your API key to `.env`:
```env
GOOGLE_MAPS_API_KEY=your_api_key_here
```
[Get a Google Maps API key](https://developers.google.com/maps/documentation/javascript/get-api-key)

## Usage

### Faker Integration
```php
class UserFactory extends Factory
{
    protected $model = User::class;

    public function definition(): array
    {
        /** @var GoogleAddress $address */
        $address = $this->faker->britishAddress();
        
        return [
            'first_name' => $this->faker->firstName(),
            'full_address' => $address->getFormattedAddress(),
            'latitude' => $address->getCoordinates()->getLatitude(),
            'longitude' => $address->getCoordinates()->getLongitude()
        ];
    }
}
```

### Facade Usage
```php
use Nonsapiens\RealAddressFactory\RealAddressFactory;

// Generate 20 Johannesburg addresses
$saAddresses = RealAddressFactory::makeSouthAfrica(20, 'Johannesburg');
```

### Adding New Countries
Update `config/realaddress.php`:
```php
'brazil' => [
    'cities' => ['Rio de Janeiro', 'São Paulo']
],
```
Then use:
```php
$faker->realAddress('Brazil', 'Rio de Janeiro');
```

## Fork Differences from Original
- ✅ Laravel 12 support
- ✅ Updated dependencies (Testbench 10.x, Geocoder 5.x)
- 🔄 Maintains original functionality
- ⚠️ Namespaces remain unchanged for compatibility

## Warning
- Google may block excessive API requests
- API usage may incur Google Cloud charges
- Built-in rate limiter configurable in `config/realaddress.php`

## Maintenance
**Current Maintainer**  
[Deon Okonkwo](mailto:deondazy@gmail.com)

**Original Author**  
[Stuart Steedman](https://github.com/nonsapiens) - CTO of [Sebenza](http://sebenza.tech)  

## Contributing
Pull requests welcome! Please open issues for:
- Laravel compatibility updates
- New country/city additions
- Documentation improvements

[View Fork Source](https://github.com/johndoe/realaddressfactory)
