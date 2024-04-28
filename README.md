# knowledge
Useful links for tech and non tech

# JAVA
Exception in thread "main" java.lang.UnsupportedClassVersionError: org/springframework/boot/SpringApplication has been compiled by a more recent version of the Java Runtime (class file version 61.0), this version of the Java Runtime only recognizes class file versions up to 59.0

Resolution: 
https://stackoverflow.com/questions/12252123/build-path-entry-is-missing-error-when-trying-to-create-a-new-project-in-eclip
1) I have installed jdk 22 on my machine and then changed JAVA_HOME and Path %JAVA_HOME%/bin variable
2) Added new JRE in eclipse Window>>Preferences>>Java>>Installed JRES .. Remove old JRE
3) Now right click Project>>Java Build Path>>Libraries>> Edit the existing JRE to Installed JRE
4) mvn clean install
   


https://www.baeldung.com/java-lang-unsupportedclassversion
 major version numbers map to Java versions:

45 = Java 1.1
46 = Java 1.2
47 = Java 1.3
48 = Java 1.4
49 = Java 5
50 = Java 6
51 = Java 7
52 = Java 8
53 = Java 9
54 = Java 10
55 = Java 11
56 = Java 12
57 = Java 13
58 = Java 14
59 = Java 15
60 = Java 16
61 = Java 17
62 = Java 18
63 = Java 19
64 = Java 20
65 = Java 21
66 = Java 22
