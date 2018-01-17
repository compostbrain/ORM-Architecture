Answer all of these questions. Write at least one paragraph per question. Send your answers to your mentor for review.
- What's a RubyGem and why would you use one?
A ruby gem is a way of packaging ruby code for reuse in other projects similar to npm packages in node.  A gem has a name, version and platform.  Inside a gem there is code (including tests), documentation and a gemspec file.  The lib directory contains the excecutable code while the spec or test directory contains tests

- What's the difference between lazy and eager loading?
Lazy loading is a design pattern that defers initialization of an object until it is needed. Eager loading is the process wewhere a query for one type of entity also loads related entities.  It is commonly used to avoid the n+1 queries problem.

- What's the difference between the CREATE TABLE and INSERT INTO SQL statements?

The difference is that CREATE TABLE defines a tables columns or attributes.  INSERT INTO is used to add rows with specific data assigned to the attributes or columns.

- What's the difference between extend and include? When would you use one or the other?


Include is for adding methods from a module to a class instance and extend is used for adding class methods. When using the include method and self.included hook include can also add class methods which can be a little confusing.


- In persistence.rb, why do the save methods need to be instance (vs. class) methods?

The save methods should be instance methods because there need to be an instantiated object to keep track of the data. If you were just calling a class method you would not have an object container for the data.

- Given the Jar-Jar Binks example earlier, what is the final SQL query in persistence.rb's save! method?

```SQL
UPDATE Characters
      SET character_name
      WHERE id = 1;
```

- AddressBook's entries instance variable no longer returns anything. We'll fix this in a later checkpoint. What changes will we need to make?

We will need methods to retrieve the values from the database.

- Write a Ruby method that converts snake_case to CamelCase using regular expressions (you can test them on Rubular). Send your code to your mentor.
```ruby
def camelize(lower_case_and_underscored_word, first_letter_in_uppercase = true)
  if first_letter_in_uppercase
    lower_case_and_underscored_word.to_s.gsub(/\/(.?)/) { "::" + $1.upcase }.gsub(/(^|_)(.)/) { $2.upcase }
  else
    lower_case_and_underscored_word.first + camelize(lower_case_and_underscored_word)[1..-1]
  end
end
```

- Add a select method which takes an attribute and value and searches for all records that match:

lib/bloc_record/selection.rb
```ruby
def find_by(attribute, value)
    # work here
    row = connection.get_first_row <<-SQL
      SELECT #{columns.join ","}
      FROM #{table}
      WHERE #{attribute} = #{value};
    SQL
    data = Hash[columns.zip(row)]
    new(data)
end
```
Assuming you have an AddressBook, it might get called like this:

```ruby
myAddressBook = AddressBook.find_by("name", "My Address Book")
```

Your code should use a SELECT…WHERE SQL query and return an array of objects to the caller. Send your code to your mentor.
