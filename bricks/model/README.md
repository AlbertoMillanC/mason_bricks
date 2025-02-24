# Model

A brick to create your model with properties and all the supporting methods, copyWith, to/from json, equatable and more!

This brick supports custom types and custom lists!

## How to use 🚀

```
mason make model --model_name user --additionals "[copyWith, json, equatable]" --style basic
```

Then add your properties! (Optional)

## Variables ✨

| Variable         | Description                                                | Default                                   | Type      |
| ---------------- | ---------------------------------------------------------- | ----------------------------------------- | --------- |
| `model_name`     | The name of the model                                      | model                                     | `string`  |
| `additionals`    | The additionals methods/extensions you can have on a model | [copyWith, json, equatable]               | `array`   |
| `style`          | The style of model                                         | basic (basic, json_serializable, freezed) | `enum`    |
| `add_properties` | Add properties                                             | true                                      | `boolean` |

## Outputs 📦

```
--model_name user --additionals "[copyWith, json, equatable]" --style json_serializable
├── user.dart
├── user.g.dart
└── ...
```

```dart
import 'package:equatable/equatable.dart';
import 'package:json_annotation/json_annotation.dart';

part 'user.g.dart';

/// {@template user}
/// User description
/// {@endtemplate}
@JsonSerializable()
class User extends Equatable {
  /// {@macro user}
  const User({
    required this.name,
    required this.familyMembers,
    required this.family,
  });

  /// Creates a User from Json map
  factory User.fromJson(Map<String, dynamic> data) => _$UserFromJson(data);

  /// A description for name
  final String name;

  /// A description for familyMembers
  final List<User> familyMembers;

  /// A description for family
  final Family family;

  /// Creates a copy of the current User with property changes
  User copyWith({
    String? name,
    List<User>? familyMembers,
    Family? family,
  }) {
    return User(
      name: name ?? this.name,
      familyMembers: familyMembers ?? this.familyMembers,
      family: family ?? this.family,
    );
  }

  @override
  List<Object?> get props => [
        name,
        familyMembers,
        family,
      ];

  /// Creates a Json map from a User
  Map<String, dynamic> toJson() => _$UserToJson(this);
}

//user.g.dart
part of 'user.dart';

User _$UserFromJson(Map<String, dynamic> json) => User(
      name: json['name'] as String,
      familyMembers: (json['familyMembers'] as List<dynamic>)
          .map((e) => User.fromJson(e as Map<String, dynamic>))
          .toList(),
      family: Family.fromJson(json['family'] as Map<String, dynamic>),
    );

Map<String, dynamic> _$UserToJson(User instance) => <String, dynamic>{
      'name': instance.name,
      'familyMembers': instance.familyMembers,
      'family': instance.family,
    };

```
