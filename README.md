# WebApi written in C# (ASP.NET Core) to find pets

Pet can have either one Owner or one Shelter

Owner can have maximum 5 pets

Shelter can have 0 or many pets.
Shelter can define which pet type and maximum capacity for that type they will have. Number of pets must be lower or equal to their maximum capacity of that pet type.

When owner wants to adopt a pet, it has to be approved by shelter. When shelter approves adoption, that owner becomes the rightful owner. In this process of adoption, shelter losses ownership of that pet and the new owner gets it.

If a shelter gets closed, then all of their pets need to be reallocated to other shelters that have available capacity.
It sends a request to other shelters and those shelters has to approve transfer. Only when shelter has no more pets can it get closed. A closed shelter cannot get new pets.

If a owner can no longer take care of a pet, then it have to select shelter that have available capacity.
It sends a request, that shelter has to approve.

# Classes and relations

class Pet
- Guid PetId
- string? Name
- Breed Breed
- string? Description
- uint Age
- Gender Gender
- Size Size
- byte[] Photo
- PetType PetType
- IOwner Owner(Can be of a type Person or Shelter)

enum Gender
- Male
- Female

enum (Enumeration)
- Small
- Medium
- Large

enum PetType
- Dog
- Cat
- Fish
- GuineaPig
- Hamster
- Rabbit
- Bird

interface Breed

class DogBreed implements Breed
class CatBreed implements Breed
class FishBreed implements Breed
class GuineaPig implements Breed
class Hamster implements Breed
class Rabbit implements Breed
class Bird implements Breed

interface IOwner
- Guid Id
- string? Name
- string? Email
- string? Phone
- Address Address
- IEnumerable<Pet> Pets

class Address
- string? Address1
- string? Address2
- string? City
- string? State
- uint Postcode
- string? Country

class Shelter implements IOwner
- bool IsClosed
- Dictionary<PetType, Capacity> Capacity

class Capacity
- uint Maximum
- uint Occupied
- bool IsAvailable

class Person implements IOwner
- uint NumberOfPets