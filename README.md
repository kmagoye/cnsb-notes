# cnsb-notes
CNSB - Cloud Native Spring Boot Action 
- This is the notes repository, responsible for executing the commands as defined in the book

- Managing different Java versions and distributions on your machine might be painful. I recommend using a tool like sdkman (https://sdkman.io) to install, update, and switch between different JDKs easily. On macOS and Linux, you can install sdkman as follows:
> curl -s "https://get.sdkman.io" | bashcurl -s "https://get.sdkman.io" | bash

- Once it’s installed, check all the available OpenJDK distributions and versions by running the following command:

> sdk list java

---
- There is this to consider
> Omit Identifier to install default version 17.0.8.1-tem:
> $ sdk install java
> Use TAB completion to discover available versions
> $ sdk install java [TAB]
> Or install a specific version by Identifier:
> $ sdk install java 17.0.8.1-tem
> Hit Q to exit this list view

Then choose a distribution and install it. For example, I can install the latest 17 version of Eclipse Temurin available at the moment of writing as follows:

$ sdk install java 17.0.3-tem

By the time you read this section, newer versions might be available, so please check the list returned from the list command to identify the latest one.

At the end of the installation procedure, sdkman will ask whether you want to make that distribution the default one. I recommend you say yes to ensure that you have access to Java 17 from all the projects you build throughout the book. You can always change the default version with the following command:

$ sdk default java 17.0.3-tem
Let’s now verify the OpenJDK installation:

$ java --version
openjdk 17.0.3 2022-04-19
OpenJDK Runtime Environment Temurin-17.0.3+7 (build 17.0.3+7)
OpenJDK 64-Bit Server VM Temurin-17.0.3+7 (build 17.0.3+7, mixed mode)
You also have the option to change the Java version only within the context of the current shell:

$ sdk use java 17.0.3-tem
Finally, if you want to check which version of Java is configured in the current shell, you can do that as follows:

$ sdk current java
Using java version 17.0.3-tem