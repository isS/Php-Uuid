Pure PHP UUID generator

Dual-licensed under BSDL (2-clause) or Apache 2.0 license 


UUID (Universally Unique Identifier) is standard (part of ISO/IEC 11578:1996) to create “universally unique” identifiers to identify objects within a system or across system boundaries. The identifiers are 128-bit in length (that’s 16 bytes) and while there really is no way to guarantee global uniqueness the probability of colissions are very small both thanks to the number of bits and the way the identifiers are created.

The UUID generation algorithms are specified in RFC4122 and I’ve created a static PHP class that implements version 1 which is time based UUID, version 4 which is truly psuedo random UUID and version 3 and 5 which are named based UUID, using either MD5 (version 3) or SHA-1 (version 5).

This class has no external dependencies.

The class has the following public functions, their return value depends on the format argument.

        $mixed generate($type, $fmt = self::FMT_BYTE, $node = "", $ns = "")
        $mixed convert($uuid, $from, $to)

UUID version constants where each constant represents a specific UUID version

        UUID_TIME, UUID_NAME_MD5, UUID_RANDOM, UUID_NAME_SHA1

UUID format constants

• FMT_BYTE is the default and returns a array of bytes that represents the 128-bit UUID.
• FMT_FIELD returns a associative array with individual fields as the format specified in RFC4122.
• FMT_STRING returns the familiar ASCII representation of a UUID (xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx).
• FMT_BINARY returns a raw 128-bit binary representation of the UUID.

The convert method can be used to convert between these representations.

#UUID version 1 example
xxxxxxxxx-xxxx-1xxx-xxxx-xxxxxxxxxxxx
Version 1 UUIDs are timed based with the node constant. The name space argument is ignored and is not used in the generation. The node identifier (”abcdef” in this case) should identify the node or object, only 6 bytes (or characters) are used from the node id.

        require_once('class.uuid.php');
        $str = UUID::generate(UUID::UUID_TIME, UUID::FMT_STRING, "abcdef");
        print "$str\n";

Example output, the last part is the node id and will remain constant (as long as the node id is the same), the first part will change according to time while the middle part is pseudo random.

    1b55e723-578b-4e34-d5cf-616263646566

The class does not fully implement version 1 as described in the RFC. The clock sequence is generated from a psuedo random generator each time a new UUID is generated and not written and read from a stable storage as described in the RFC.

#UUID version 4 example
xxxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx
Version 4 is a fully pseudo random where all fields are randomly generated.

        require_once('class.uuid.php');
        $str = UUID::generate(UUID::UUID_RANDOM, UUID::FMT_STRING);
        print "$str\n";

Kind of useless example output

    d8988842-43d5-42b3-9049-af4bbc694dbe

#UUID version 3/5 example

xxxxxxxxx-xxxx-3/5xxx-xxxx-xxxxxxxxxxxx
The main difference is that a node id is unique within a name space and a UUID generated from the same node id and name space is always the same. The generation algorithm is the same for both version 3 and 5 with the only difference being the hash method used (MD5 versus SHA1).
This is the example from the RFC.

        require_once('class.uuid.php');

        /*
         * 6ba7b810-9dad-11d1-80b4-00c04fd430c8 is the DNS name space
         */
        $md5 = UUID::generate(UUID::UUID_NAME_MD5, UUID::FMT_STRING,
            "www.widgets.com", '6ba7b810-9dad-11d1-80b4-00c04fd430c8');
        $sha1  = UUID::generate(UUID::UUID_NAME_SHA1, UUID::FMT_STRING,
            "www.widgets.com", '6ba7b810-9dad-11d1-80b4-00c04fd430c8');
        print "MD5: $md5\n";
        print "SHA1: $sha1\n";

Example output

    MD5: e902893a-9d22-3c7e-a7b8-d6e313b71d9f
    SHA1: 13726f09-44a9-5eeb-8910-3525a23fb23b

#Final notes

This class have been tested with PHP 5.2.x on both little and big endian machines. While there could be bugs in the algorithm implementation at least they are consistent across platforms