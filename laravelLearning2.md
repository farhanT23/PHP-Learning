# More Learning

## Eloquent: Mutators & Casting

# 🔥 First, the Main Idea

- **Mutators** = Modify data **before saving** to database or **after fetching** from database.
- **Casting** = Tell Laravel how to **automatically convert** your database fields into PHP types (array, boolean, date, etc).

They make your Eloquent models *smarter*, *cleaner*, and *easier to work with*.

---

# 🛠️ Mutators

---

## ➡️ 1. What is a Mutator?

> A **mutator** automatically **modifies** the value when you **get** or **set** a property on your Eloquent model.

Two types:
- **Get Mutator** ➔ changes value when you **access** it.
- **Set Mutator** ➔ changes value when you **assign** it.

---

## ➡️ 2. Example: Set Mutator

Imagine you want every user's **name** saved **with first letter capitalized**.

```php
class User extends Model
{
    protected $fillable = ['name'];

    // Set Mutator
    public function setNameAttribute($value)
    {
        $this->attributes['name'] = ucfirst($value);
    }
}
```

✅ Now, when you do:

```php
$user = new User();
$user->name = 'john';   // You set 'john'
$user->save();
```

**In the database**, it saves: `John` ✅

---

## ➡️ 3. Example: Get Mutator

Imagine you want **user name** always returned in **uppercase** when you read it:

```php
class User extends Model
{
    // Get Mutator
    public function getNameAttribute($value)
    {
        return strtoupper($value);
    }
}
```

✅ Now, when you do:

```php
$user = User::find(1);
echo $user->name;   // Outputs: JOHN
```

Even though database has `John`, you always *see* it as `JOHN` in your app.

---

# 🧬 Casting

---

## ➡️ 1. What is Casting?

> **Casting** automatically **converts** database values into **specific PHP types** when you retrieve them.

It’s like telling Laravel:

> "*Hey, whenever you load this column, treat it as an array!*"

---

## ➡️ 2. Common Types You Can Cast

- `integer`
- `boolean`
- `array`
- `object`
- `date`
- `datetime`
- `encrypted` (auto encrypt/decrypt)
- etc.

---

## ➡️ 3. Example: Boolean Cast

Suppose your `users` table has a column `is_admin` (0 or 1).  
You want `$user->is_admin` to behave like **true/false** in PHP automatically.

```php
class User extends Model
{
    protected $casts = [
        'is_admin' => 'boolean',
    ];
}
```

✅ Now:

```php
$user = User::find(1);

if ($user->is_admin) {
    // true
}
```

Even though database stores `0` or `1`, you get real PHP `true` or `false` automatically!

---

## ➡️ 4. Example: Array Cast

Suppose you store multiple phone numbers as JSON in database:

```php
class User extends Model
{
    protected $casts = [
        'phone_numbers' => 'array',
    ];
}
```

✅ Now:

```php
$user = User::find(1);

foreach ($user->phone_numbers as $phone) {
    echo $phone;
}
```

Laravel automatically **decodes JSON** into **PHP array**! 🪄

---

#  Tip

- Use **Mutators** when you want to **control the value** going *in* or *out*.
- Use **Casts** when you want **automatic type conversion** *without manual work*.
- Laravel 12 makes code even simpler with **attribute objects** (new syntax), but concept is same.

---

# 🚀 Bonus: New Laravel 12 Syntax (Attribute Casting)

Now in Laravel 12, you can define mutators *cleaner* using `Attribute` class:

```php
use Illuminate\Database\Eloquent\Casts\Attribute;

class User extends Model
{
    public function name(): Attribute
    {
        return Attribute::make(
            get: fn ($value) => strtoupper($value),
            set: fn ($value) => ucfirst($value),
        );
    }
}
```

Same effect — cleaner, modern ✨

---

# 🎯 Conclusion:

✅ **Mutators** modify when saving or retrieving.  
✅ **Casts** auto-convert field types without manual code.  
✅ They both make your Laravel models more **powerful**, **simple**, and **automatic**.
