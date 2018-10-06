# English Words  Provider for PHP's Faker Library

#### Why English words? Let me explain.
First of all, look at this [link](https://stackoverflow.com/questions/33270023/php-faker-how-to-create-n-unique-words)

Basically, the default [Lorem](https://github.com/fzaninotto/Faker/blob/master/src/Faker/Provider/Lorem.php) provider that comes with the library is very limited when generating __unique__ words. The internal lorem-ipsum words-list comes with 182 unique words only. 

This provider does just one thing: It extends the default Lorem provider, and changes the word-list with English words (I got the dictionary from [here](https://github.com/dwyl/english-words), I removed a couple of lines however), which contain about __400k__ words.

#### Usage
```php
// Assuming everything is auto-loaded
// Create faker
$faker = Faker\Factory::create();
// Just make sure the default Lorem provider is not added after this. 
$faker->addProvider(new BReda\Faker\Provider\EnglishWords($faker));
```

---

#### Let's test it out
This will throw this exception
Fatal error:  Uncaught OverflowException: Maximum retries of 10000 reached without finding a unique value
```php
// Create faker
$faker = Faker\Factory::create();

foreach(range(0, 2000) as $i) {
    echo $faker->unique()->word;
}
```

This will not throw an exception and will successfully print 200,000 unique words from the English language.
```php
// Create faker
$faker = Faker\Factory::create();
$faker->addProvider(new BReda\Faker\Provider\EnglishWords($faker));

foreach(range(0, 200000) as $i) {
    echo $faker->unique()->word;
}
```

And that's it!