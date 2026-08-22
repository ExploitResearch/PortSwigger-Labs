# Insecure Deserialization

Insecure deserialization occurs when an application deserializes untrusted data without proper validation. This can allow attackers to manipulate serialized objects to bypass authentication, escalate privileges, or achieve remote code execution via gadget chains.

**Common serialization formats:**
- PHP: `serialize()` / `unserialize()`
- Java: `ObjectInputStream` / `ObjectOutputStream`
- Ruby: `Marshal.dump` / `Marshal.load`
- Python: `pickle.dumps` / `pickle.loads`
- .NET: `BinaryFormatter`

## Labs

- [Arbitrary object injection in PHP](./Arbitrary_object_injection_in_PHP.md)
- [Developing a custom gadget chain for Java deserialization](./Developing_a_custom_gadget_chain_for_Java_deserialization.md)
- [Developing a custom gadget chain for PHP deserialization](./Developing_a_custom_gadget_chain_for_PHP_deserialization.md)
- [Exploiting Java deserialization with Apache Commons Collections](./Exploiting_Java_deserialization_with_Apache_Commons_Collections.md)
- [Exploiting PHP deserialization with a pre-built gadget chain](./Exploiting_PHP_deserialization_with_a_pre-built_gadget_chain.md)
- [Exploiting Ruby deserialization using a documented gadget chain](./Exploiting_Ruby_deserialization_using_a_documented_gadget_chain.md)
- [Modifying serialized data types](./Modifying_serialized_data_types.md)
- [Modifying serialized objects](./Modifying_serialized_objects.md)
- [Using PHAR deserialization to deploy a custom gadget chain](./Using_PHAR_deserialization_to_deploy_a_custom_gadget_chain.md)
- [Using application functionality to exploit insecure deserialization](./Using_application_functionality_to_exploit_insecure_deserialization.md)
