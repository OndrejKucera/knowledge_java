Input/Output
===========================

## Handling Data Formats
### String
* String class is handled in a special way for easy use. Literal `String` is an object.
* 4 ways how to concatenate an String - plus operator, or `StringBuilder` (`StringBuffer` for concurrency), `String.concat()`
* String is **immutable** - It saves memory and use **String pool**, security reason (file can’t be corrupted), it can be safely shared between threads, String is final class (except of `hash` - effectively immutable) and can be used as key in HashMap (hashcode is saved -> fast)
* Hashcode - Java calculates it only when it is needed and then cash the value for later use.
* String and password - It is better to use char[]. The string is held in memory for a long time, it is immutable and therefore can be read later (i.e. memory dump). On other hand char[] can be erased, no risk to print it in logs.
* **String pool** lives on Heap
### Regular expressions
 * Class `Pattern` is used (`java.util.regex`)
 * Pattern has method `asPredicate()` (since Java 8) for lambda expression
 * `?` optional char, `*` zero or more char, `+` one or more char, `.` any single char
 * `/d` digit, `/D` non-digit
 * `/w` word, `/W` nonword
 * `/s` whitespace `/S` non-whitespace
 * `/n` new line char, `/t` tab char
 * `{M, N}` between M and N of previous char
 * `[ ]` any char in bracket, `[^ ]` any char not in bracket
 * `( )` group of patterns
 * `|` alternative (OR)
 * `^` start of string, `$` end of string
### Numbers
 * Integers types are all signed (represent negative and positive numbers)
 * `BigDecimal` has exact way of representing numbers (floating point error) and it is slower than Double
 
## Handling I/O and File
 * `File` is a cornerstone of an original way to do file i/o and represents file or directory. It has lots of methods
 * `Stream` is the sequential stream of bytes from disk or other sources. Abstract subclasses are `InputStream` and `OutputStream` then there are more specific `FileInputStream` or `FileOutputStreams`. It is dealing with the lack of flexibility. Often it is combined with `Reader` or `Writer` classes that provide character stream level of interaction.
 * **The Modern I/O**
    * brand new API for i/o called **NIO.2**, package - `java.nio.file`
    * Files:
      * `File.createFile(target, attributes)`
      * `File.delete(target)`
      * `File.copy(source, target)`
      * `File.move(source, target)`
      * `File.isDirectory(target)`
      * `File.isSymbolicLink(target)`
      * `File.readAllLines(target, cs)`
      * `File.readAllBytes(target)`
    * Paths - has to `get()` method for creating `Path` object. The path is abstract representing file location.
    * ByteBuffer - sequence of bytes 
    * Chanels
