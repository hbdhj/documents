
# static_cast   

static_cast is the first cast you should attempt to use. It does things like implicit conversions between types (such as int to float, or pointer to void*), and it can also call explicit conversion functions (or implicit ones). In many cases, explicitly stating static_cast isn't necessary, but it's important to note that the T(something) syntax is equivalent to (T)something and should be avoided (more on that later). A T(something, something_else) is safe, however, and guaranteed to call the constructor.

static_cast can also cast through inheritance hierarchies. It is unnecessary when casting upwards (towards a base class), but when casting downwards it can be used as long as it doesn't cast through virtual inheritance. It does not do checking, however, and it is undefined behavior to static_cast down a hierarchy to a type that isn't actually the type of the object.

# const_cast

const_cast can be used to remove or add const to a variable; no other C++ cast is capable of removing it (not even reinterpret_cast). It is important to note that modifying a formerly const value is only undefined if the original variable is const; if you use it to take the const off a reference to something that wasn't declared with const, it is safe. This can be useful when overloading member functions based on const, for instance. It can also be used to add const to an object, such as to call a member function overload.

const_cast also works similarly on volatile, though that's less common.

# dynamic_cast

dynamic_cast is almost exclusively used for handling polymorphism. You can cast a pointer or reference to any polymorphic type to any other class type (a polymorphic type has at least one virtual function, declared or inherited). You can use it for more than just casting downwards -- you can cast sideways or even up another chain. The dynamic_cast will seek out the desired object and return it if possible. If it can't, it will return nullptr in the case of a pointer, or throw std::bad_cast in the case of a reference.

dynamic_cast has some limitations, though. It doesn't work if there are multiple objects of the same type in the inheritance hierarchy (the so-called 'dreaded diamond') and you aren't using virtual inheritance. It also can only go through public inheritance - it will always fail to travel through protected or private inheritance. This is rarely an issue, however, as such forms of inheritance are rare.

# reinterpret_cast

reinterpret_cast is the most dangerous cast, and should be used very sparingly. It turns one type directly into another - such as casting the value from one pointer to another, or storing a pointer in an int, or all sorts of other nasty things. Largely, the only guarantee you get with reinterpret_cast is that normally if you cast the result back to the original type, you will get the exact same value (but not if the intermediate type is smaller than the original type). There are a number of conversions that reinterpret_cast cannot do, too. It's used primarily for particularly weird conversions and bit manipulations, like turning a raw data stream into actual data, or storing data in the low bits of an aligned pointer.

# C cast

C casts are casts using (type)object or type(object). A C-style cast is defined as the first of the following which succeeds:

   const_cast
   static_cast (though ignoring access restrictions)
   static_cast (see above), then const_cast
   reinterpret_cast
   reinterpret_cast, then const_cast

It can therefore be used as a replacement for other casts in some instances, but can be extremely dangerous because of the ability to devolve into a reinterpret_cast, and the latter should be preferred when explicit casting is needed, unless you are sure static_cast will succeed or reinterpret_cast will fail. Even then, consider the longer, more explicit option.

C-style casts also ignore access control when performing a static_cast, which means that they have the ability to perform an operation that no other cast can. This is mostly a kludge, though, and in my mind is just another reason to avoid C-style casts.
