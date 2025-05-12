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

----

## Laravel Testing
### Video with good explaination: [Link To Tutorial](https://www.youtube.com/watch?v=ozsumbtTqpw)

## OAuth 2.0

- OAuth stands for Open Authorization
- The OAuth protocol was developed as a solution for granting access to a limited set of resources for a predefined period of time without sharing usernames and passwords.

***The client***
When dealing with OAuth, you’ll often come across the terms “client” or “client_id.” In this context, the client does not refer to an end-user or customer.

The term “client” does not mean “end-user” or “customer” in this case. Instead, the term “client” is used to refer to the application that obtaining access to the protected resources.

***Resources***
A client has resources which are protected with the OAuth protocol. Often, with resources, we mean API-endpoints.

***The authorisation server***
The authorization server is where the client requests the end-user to authenticate and obtain a token that represents the scope of permissions granted to the client. During this process:

- The user provides their username and password on the authorization server.
- The user can consent or deny access to specific resources based on the application’s request, though this feature may be disabled in some cases.

Only registered clients can request end-users to authenticate, ensuring secure access management.

***The end-user***
OAuth is designed to grant access to resources on behalf of someone or something. The end-user can be a person, but the protocol also supports machine-to-machine communication.

This is why there is not too many emphasis on the term “end-user” in the documentation.

## Larvel Socialite
### VideoLink for better; [Tutorial](https://www.youtube.com/watch?v=p0I25hL3pBI)


## Laravel Eloquent ORM

### Polymorphic Relationship



### 💡 **What Are Polymorphic Relationships?**

A polymorphic relationship allows a model to belong to more than one other model on a **single association**.

#### 📝 **Example Scenario:**

Imagine you have a system where:

* **Posts** and **Videos** can both have **comments**.
* Instead of creating separate `comments` tables for each, you use **one `comments` table** with a polymorphic relationship.

---

## 🚀 **Step 1: Setting Up the Models and Migration**

### 1. **Creating the Models and Migrations**

```bash
php artisan make:model Post -m
php artisan make:model Video -m
php artisan make:model Comment -m
```

---

### 2. **Updating the Migrations**

#### 📂 **Posts Migration:**

```php
// database/migrations/xxxx_xx_xx_create_posts_table.php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('body');
    $table->timestamps();
});
```

#### 📂 **Videos Migration:**

```php
// database/migrations/xxxx_xx_xx_create_videos_table.php
Schema::create('videos', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->string('url');
    $table->timestamps();
});
```

#### 📂 **Comments Migration:**

```php
// database/migrations/xxxx_xx_xx_create_comments_table.php
Schema::create('comments', function (Blueprint $table) {
    $table->id();
    $table->text('body');
    $table->morphs('commentable');  // Creates commentable_id and commentable_type
    $table->timestamps();
});
```

#### 💡 **Why `morphs()`?**

The `morphs()` method is a **shortcut** that creates:

* `commentable_id` (integer)
* `commentable_type` (string)
  These two columns determine **which model** the comment belongs to.

---

## 🚀 **Step 2: Defining Relationships in Models**

### 📂 **Post Model:**

```php
// app/Models/Post.php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\MorphMany;

class Post extends Model
{
    protected $fillable = ['title', 'body'];

    public function comments(): MorphMany
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}
```

### 📂 **Video Model:**

```php
// app/Models/Video.php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\MorphMany;

class Video extends Model
{
    protected $fillable = ['title', 'url'];

    public function comments(): MorphMany
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}
```

### 📂 **Comment Model:**

```php
// app/Models/Comment.php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\MorphTo;

class Comment extends Model
{
    protected $fillable = ['body'];

    public function commentable(): MorphTo
    {
        return $this->morphTo();
    }
}
```

---

## 🚀 **Step 3: Migrating the Database**

```bash
php artisan migrate
```

---

## 🌟 **Step 4: Seeding Some Data**

### 📂 **DatabaseSeeder:**

```php
// database/seeders/DatabaseSeeder.php
use App\Models\Post;
use App\Models\Video;
use App\Models\Comment;

Post::factory()->count(3)->create()->each(function ($post) {
    $post->comments()->create(['body' => 'This is a comment on a post']);
});

Video::factory()->count(2)->create()->each(function ($video) {
    $video->comments()->create(['body' => 'This is a comment on a video']);
});
```

```bash
php artisan db:seed
```

---

## 🚀 **Step 5: Retrieving the Data**

### 📂 **Route Example:**

```php
// routes/web.php
use App\Models\Post;
use App\Models\Video;

Route::get('/comments', function () {
    $post = Post::with('comments')->first();
    $video = Video::with('comments')->first();

    return [
        'Post Comments' => $post->comments->pluck('body'),
        'Video Comments' => $video->comments->pluck('body')
    ];
});
```

#### 📝 **Explanation:**

* `with('comments')` eagerly loads comments related to a **post** or **video**.
* `pluck('body')` retrieves only the comment text.

---

## 🌐 **Step 6: Testing the Output**

Visit:

```
http://localhost:8000/comments
```

#### 💡 **Expected Output:**

```json
{
    "Post Comments": ["This is a comment on a post"],
    "Video Comments": ["This is a comment on a video"]
}
```

---

## 🔄 **Why Use Polymorphic Relationships?**

1. **Reusability:**

   * The `Comment` model is **not tied to any specific model**, making it flexible.
2. **Efficiency:**

   * Instead of creating separate comment tables for posts, videos, and other entities, **one table** does the job.
3. **Simplicity:**

   * Easy to query comments for **different models** in a unified way.

---

## 📝 **Advanced Usage - Reverse Lookups**

To find which model a comment belongs to:

```php
$comment = Comment::first();
echo $comment->commentable; // Returns either a Post or Video instance
```

---

## 💡 **Key Takeaways:**

* **Polymorphic relationships** save you from having multiple **redundant tables**.
* **Dynamic associations** are easy to manage and scale.
* Perfect for scenarios where **multiple models share a similar relationship** (like comments, tags, likes).


### Has-One-Of-Many

### 💡 **What is a Has-One-Of-Many Relationship?**

Imagine you have a **user** who has **many orders**. Sometimes, you don't need to see **all orders**—you just want to know:

* **The latest order** the user made.
* **The most expensive order** the user made.

Instead of writing **complex queries** every time to get just one specific order, Laravel provides a shortcut:
**`Has-One-Of-Many` relationship**!
It helps you **automatically pick one order** from many, based on a condition (like the latest or highest).

---

## 🗂️ **Think of it like this:**

Imagine you have a box of receipts (orders) for a user:

1. You only want the **latest receipt** from the box.
2. Or, you want the **receipt with the highest amount**.
   Instead of going through all the receipts every time, you just set a **rule** that automatically picks the right one for you!

---

## 🛠️ **How Do We Set This Up?**

### Step 1: **Create the Models and Database Tables**

1. **User Model:** Represents the customer.
2. **Order Model:** Represents the purchases made by the customer.

#### User Model

```php
class User extends Model
{
    // Latest order made by the user
    public function latestOrder()
    {
        return $this->hasOne(Order::class)->latestOfMany('ordered_at');
    }

    // Most expensive order made by the user
    public function highestOrder()
    {
        return $this->hasOne(Order::class)->ofMany('amount', 'max');
    }
}
```

---

### 📝 **Why Write It Like This?**

* **`latestOfMany('ordered_at')`:**

  * It tells Laravel to **pick the most recent order** from all orders based on the `ordered_at` date.
* **`ofMany('amount', 'max')`:**

  * It tells Laravel to **pick the order with the highest amount** from all orders.

---

### 🗂️ **Step 2: Store Some Orders**

Imagine you have a user named John. You add three orders:

* **Order 1:** Amount = \$100, ordered at **5 days ago**
* **Order 2:** Amount = \$250, ordered at **2 days ago**
* **Order 3:** Amount = \$150, ordered at **1 day ago**

---

### 📝 **Why Do We Need This?**

* If you always want the **latest order**, you don’t need to sort them every time.
* If you want the **highest value order**, you don’t need to scan the entire list.
* You can just **get the data directly** using the relationship!

---

## 🔥 **How Do We Use It?**

Now let's **fetch and display the orders**:

```php
$user = User::first();

echo "Latest Order: " . $user->latestOrder->amount; // Output: 150 (latest order)
echo "Highest Order: " . $user->highestOrder->amount; // Output: 250 (highest order)
```

---

### 🤔 **Why Does This Work So Well?**

1. **Automatic Filtering:**

   * Laravel automatically **applies the rule** (latest or highest) when you call the relationship.
2. **Performance:**

   * Instead of loading **all orders** and then filtering them, it **directly fetches the needed one**.
3. **Readable Code:**

   * Instead of writing a query like this:

     ```php
     $latestOrder = $user->orders()->orderBy('ordered_at', 'desc')->first();
     $highestOrder = $user->orders()->orderBy('amount', 'desc')->first();
     ```
   * You just write:

     ```php
     $user->latestOrder;
     $user->highestOrder;
     ```

---

## 📝 **Summary:**

* The **Has-One-Of-Many** relationship helps you pick **just one item** from many based on a rule (like **latest** or **highest**).
* You define this rule in the **User model**.
* You use it when you **always need just one specific item** (like the most recent order).
* It keeps your **code simple and efficient**.


Alright, let’s dive into **HasOneThrough** and **HasManyThrough** relationships! I’ll break them down in a simple and clear way.

---

### 🌟 **What are HasOneThrough and HasManyThrough Relationships?**

These relationships are useful when:

* You want to **access a related model through another intermediate model**.
* Think of them as **"shortcut" relationships** to reach a related model without needing to directly link them.

---

## 🌱 **Scenario 1: HasOneThrough Relationship**

**When to Use:**

* When **one model is related to one other model** through **one intermediate model**.
* **Example:** A **Country** has **one Capital City** through a **State**.

---

### 💡 **Visual Representation:**

```
Country (hasOneThrough) -> State (hasOne) -> CapitalCity
```

### 🗂️ **Tables:**

* **countries:** id, name
* **states:** id, country\_id, name
* **capital\_cities:** id, state\_id, name

---

### 📝 **Setting Up Models:**

#### **Country Model:**

```php
class Country extends Model
{
    public function capitalCity()
    {
        return $this->hasOneThrough(CapitalCity::class, State::class);
    }
}
```

* **Why Use `hasOneThrough`?**

  * The **Country** doesn’t directly know about the **Capital City**.
  * But it knows a **State**, and the **State** knows its **Capital City**.
  * The `hasOneThrough` tells Laravel to **make this connection for you**.

---

#### **State Model:**

```php
class State extends Model
{
    public function capitalCity()
    {
        return $this->hasOne(CapitalCity::class);
    }
}
```

---

#### **CapitalCity Model:**

```php
class CapitalCity extends Model
{
    //
}
```

---

### 🗃️ **How to Use:**

```php
$country = Country::find(1);
echo "Capital City: " . $country->capitalCity->name;
```

* This will automatically find the **capital city** through the **state**.
* No need to manually link **Country -> State -> CapitalCity** every time.

---

---

## 🌱 **Scenario 2: HasManyThrough Relationship**

**When to Use:**

* When **one model is related to many other models** through **an intermediate model**.
* **Example:** A **University** has **many Students** through **Departments**.

---

### 💡 **Visual Representation:**

```
University (hasManyThrough) -> Department (hasMany) -> Student
```

### 🗂️ **Tables:**

* **universities:** id, name
* **departments:** id, university\_id, name
* **students:** id, department\_id, name

---

### 📝 **Setting Up Models:**

#### **University Model:**

```php
class University extends Model
{
    public function students()
    {
        return $this->hasManyThrough(Student::class, Department::class);
    }
}
```

* **Why Use `hasManyThrough`?**

  * The **University** has **many Departments**.
  * Each **Department** has **many Students**.
  * You want to **directly access all students** of a university **without manually linking departments**.

---

#### **Department Model:**

```php
class Department extends Model
{
    public function students()
    {
        return $this->hasMany(Student::class);
    }
}
```

---

#### **Student Model:**

```php
class Student extends Model
{
    //
}
```

---

### 🗃️ **How to Use:**

```php
$university = University::find(1);
foreach ($university->students as $student) {
    echo "Student: " . $student->name . PHP_EOL;
}
```

* This will directly list **all students** belonging to the **university**.
* No need to manually get **departments** first.

---

## 💡 **Summary:**

1. **HasOneThrough:**

   * Used when a model **has one** related model **through** another model.
   * Example: **Country -> State -> CapitalCity**

2. **HasManyThrough:**

   * Used when a model **has many** related models **through** another model.
   * Example: **University -> Department -> Students**

### ✅ **Why Use These Relationships?**

* They make your code **simpler and cleaner**.
* No need to **manually chain relationships**.
* Great for situations where you need to **jump over an intermediate model**.
