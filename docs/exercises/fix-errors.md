# Beheben von häufigen Fehlern

## Public Tests
### Verstehen der Resultate

Wenn Sie für eines der in den von uns bereitgestellten Public Tests gegebenen Kriterien nicht die höchstmögliche Punktzahl erreichen,
ist Ihre Lösung wahrscheinlich nicht vollständig korrekt.

Keine Sorge!
Glücklicherweise sind die Resultate unserer Public Tests so aufgebaut,
dass Sie Ihre Fehler selber verstehen können.
In Ihrem Resultat finden Sie zu jedem in Ihrer Lösung nicht-erfüllten Kriterium eine Beschreibung sowie einen für Ihre Lösung individuell erstellten Kommentar.
Beachten Sie die folgenden Hinweise zum Verstehen der Resultate.

##### Beschreibung

Die Beschreibung eines Kriteriums finden Sie in der Spalte *Kriterium*.

Um einen Fehler beheben zu können,
müssen Sie die Bedeutung des jeweilige Kriterium verstanden haben.

!!! info ""
    Ein Kriterium kann auch dann nicht erfüllt sein,
    wenn Ihre Implementation einen Fehler enthält,
    der das Überprüfen Ihrer Lösung verhindert!
    Sie werden im Kommentar auf solche Fehler hingewiesen.

    Informationen zu solchen Fehlern finden Sie aut der Abschnitt [Typische Programmierfehler]

##### Kommentar

Der Kommentar eines Kriteriums startet mit einer kurzen Fehlermeldung darüber,
wieso das jeweilige Kriterium nicht erfüllt wurde.

!!! warning ""
    Sie müssen diese Fehlermeldung *unbedingt* verstanden haben,
    bevor Sie diesen Fehler sinnvoll beheben können!


Nach dieser Fehlerbeschreibung folgen in der Regel Informationen darüber,
mit welchen Eingabedaten Ihr Programm getestet wurde.
Diese Informationen können bereits in der Fehlermeldung enthalten sein.

Versuchen Sie,
Ihr Programm mit den gegebenen Eingabedaten selber auszuführen und das Verhalten des Programms zu beobachten.
Hierbei kann es nützlich sein,
[Debugging] anzuwenden.


!!! warning "Sind die Public Tests fehlerhaft?"
    Alle von uns bereitgestellten Public Tests wurden selbstverständlich getestet.

    In wenigen Fällen unterstützt ein Public Test nicht alle gängigen mit bis zur Bearbeitung vorgestellten Inhalten aus der Vorlesung umgesetzten Implementationen.
    Solche Probleme könnten mit neuen Versionen der Vorlage behoben sein.
    Beachten Sie die Seite [Aktualisieren der Vorlage].




## Typische Programmierfehler

###### NullPointerException 

Dieser Fehler tritt immer dann auf, wenn man auf einer Variable eine Methode aufruft, oder ein auf ein Attribut zugreift, die Variable aber null ist, also ihr kein Wert zugewiesen wurde. Anbei finden Sie ein paar Beispiele wie diser Fehler entstehen kann:

```` java linenums="1"
public class MyRobot {
    // robby wird mit null initialisiert, da keine explizite Zuweisung stattfindet
    Robot robby;
    public void nullPointer1() {
        Robot robot = null;
        // Variable robot ist null
        // beim Aufruf von move wird eine eine NullPointerException geworfen
        robot.move();
    }
    public void nullPointer2() {
        // Attribut robby is null
        // beim Aufruf von move wird eine NullPointerException geworfen
        robby.move();
    }
    public void nullPointer3() {
        // neue lokale Variable wird erzeugt anstatt Objektattribut zuzuweisen
        // nullPointer2() würde nach Aufruf von nullPointer3 weiterhin NullPointerException werfen
        Robot robby = new Robot(0,0);
    }
}
````
 
 Bei allen drei Aufrufen der move Methode ist die Variable, bzw. das Attribut, auf dem die Methode aufgerufe wird null, wodurch effektiv dort steht null.move(). Da null keinem korrekt initialisiertem Objekt entspricht wirft dies eine NullPointerException. Der geworfene Fehler sieht dabei in etwa wie folgt aus:

````
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "example.Robot.move()" because "robot" is null
at example.MyRobot.nullPointer1(MyRobot.java:6)
at example.Main.main(Main.java:18)
````

###### Weitere Fehler

Diese Seite wird bald um weitere Fehler ergänzt.

## Debugging

Debugging beschreibt unter anderem das Beheben von Fehlern in Quelltexten.

### Debugging mit Stil

IntelliJ bietet Ihnen mit dem Debugger eine sehr hilfreiche Methode Fehler in Ihrem Code zu finden.
Sie können den Debugger genauso starten, wie Sie Ihren Code mit den Ihnen bekannten Methoden ausführen.
Der Unterschied ist,
dass Sie anstatt auf das *grüne Dreieck* `Run ...` auf den *roten Käfer* `Debug ...` drücken.

##### Breakpoints

Wenn Sie den Debugger starten, wird er Ihren Code so lange normal ausführen, bis er an einem Breakpoint ankommt.
In dem Fall wird das Programm angehalten und Ihnen wird eine Liste der Attribute mit aktuellen Zuweisungen angezeigt.

Mit einem Linksklick direkt neben der Zeilenangabe können Sie einen solchen Breakpoint erstellen.
Dieser wird als roter Kreis angezeigt.

##### Aktionen

Alle Aktionen können auch mittels der Tasten am oberen Rand des Debugger-Bereichs ausgeführt werden.

* Mit `F8` können Sie die momentane Zeile ausführen.
* Mit `F7` können Sie die in die Methode, die als nächstes ausgeführt wird, hineinspringen.
* Mit `F9` können Sie das Programm bis zum nächsten Breakpoint weiterlaufen lassen.
* Mit `Shift + F8` können Sie das Programm weiterlaufen lassen, bis die momentane Methode verlassen wird.

### Der Unsaubere

Für den Fall,
dass Ihnen das Debugging mittels Debugger zu schwierig erscheint,
möchten wir Ihnen einen unsauberen Klassiker vorstellen:

```java
System.out.println("my string");
```

Mit diesem Statement teilen Sie mit,
dass beim Ausführen des Programms an der jeweiligen Stelle im Programm eine Nachricht in der Konsole ausgegeben werden soll.
Sie können innerhalb der runden Klammern jeden beliebigen String einsetzen.

#### Warum sollte ich das tun?

Sie können ein Print-Statement beispielsweise dann benutzen,
wenn Sie sich eine der folgenden Fragen stellen.

* Wird dieser Teil meines Programms ausgeführt?
* Was ist diesem Attribut an dieser Stelle meines Programms zugewiesen?
* Ist diese Bedingung an dieser Stelle meines Proramms erfüllt?
* Befindet sich mein Programm in einer Endlosschleife/-rekursion?

#### Beispiel

```java
public int doStuff(int n) {

    System.out.println("n: " + n);
    System.out.println("crazyness > 1337: "crazyness > 1337)
    while (crazyness <= 9000) {
        System.out.println("current crazyness: " + crazyness);
        doCrazyStuff();
    }
    if (crazyness % 1337 == 42) {
        System.out.println("big red button pressed");
        pressBigRedButton();
        
    }
    int r = crazyness - n;
    System.out.println("return: " + r)
    return r;
}
```

## Technische Fehler

* Stellen Sie zunächst sicher, dass Sie den richtigen Ordner importiert haben. Der oberste Ordner sollte nach der Hausübung benannt sein (z. B. **"FOP-2223-HXX-Student-master"**) und direkt die build.gradle.kts Datei enthalten sein. Wählen Sie beim Importieren **nicht** einen identisch benannten Oberordner aus.
* Beachten Sie, dass es mit Gradle zu Problemen kommen kann, wenn das Projekt auf einer externen Festplatte gespeichert wurde.
* Anbei finden Sie ein paar mögliche Fehler, welche Ihnen in der Konsole, die sich beim Ausführen der des Programmes oder einer Gradle Task automatisch öffnet, angezeigt werden. Damit Ihnen die vollständigen Fehlermeldungen angezeigt werden, wählen Sie links von der Konsole die zweite Option von oben aus.



### Häufige Fehlermeldungen

1. !!! error ""
    ```
    [...] finished with non-zero exit value 1
    ```
    Diese Meldung sagt ihnen nur, dass ein Fehler aufgetreten ist. Wenn der eigentliche Fehler nicht angezeigt wird, drücken Sie links neben der Konsolenausgabe auf die zweite Option von oben. Diese sollte **":run"** oder **":<Mainclass\>:main()"** heißen.


2. !!! error ""
    ```
    A problem occurred configuring root project 'FOP-2223-H00-Student'.
    Could not resolve all files for configuration ':classpath'.
    Could not resolve org.tudalgo:algomate:0.1.0-SNAPSHOT.
    ```
    oder
    ```
    Execution failed for task ':compileJava'.
    error: invalid source release: 17
    ```
    oder
    ```
    UnsupportedClassVersionError
    ```
    oder
    ```
    [...] has been compiled by a more recent version of the Java Runtime
    ```
    Es wird eine falsche Java Version benutzt. Siehe [Korrekte Java Version in IntelliJ Einstellen].


3. !!! error ""
    ```
    Deprecated Gradle features were used in this build, making it incompatible with Gradle 8.0.
    ```
    oder
    ```
    org.junit.platform.launcher.core.EngineDiscoveryOrchestrator lambda$logTestDescriptorExclusionReasons$7
    INFO: 0 containers and 1 tests were Method or class mismatch
    ```
    Sie können diese Meldung ignorieren.


4. !!! error ""
    ```
    Execution failed for task ':mainBuildSubmission'.
    There were some errors preparing your submission. The following required properties were not set:
    studentId
    firstName
    lastName
    ```
    Sie haben vergessen, Ihre persönlichen Daten in der build.gradle.kts Datei hinzuzufügen. Siehe [Anleitung zum Exportieren].


5. !!! error ""
    ```
    execution failed for task ':test'.
    There were failing tests.
    ```
    Ihre selbstgeschriebenen Tests laufen nicht erfolgreich durch. Um dies zu beheben, fixen Sie entweder den Fehler, der in Ihren Tests auftritt, oder ändern Sie in der build.gradle.kts Datei direkt unter Ihren persönlichen Daten requireTests von true auf false:
    ```
    requireTests = false
    ```

6. !!! error ""
    ```
    execution failed for task ':graderPublicRun'.
    There were failing tests.
    ```
    Die von uns zur Verfügung gestellten public-Tests laufen nicht erfolgreich durch. Um dies zu beheben, fixen Sie entweder den Fehler, den die Tests aufzeigen, oder ändern Sie in der build.gradle.kts Datei direkt unter Ihren persönlichen Daten requirePublicTests von true auf false:
    ```
    requireGraderPublic = false
    ```

7. !!! error ""
    ```
    Execution failed for task ':compileJava'.
    Compilation failed; see the compiler error output for details.
    ```
    Es befinden sich vermutlich noch Syntaxfehler in Ihren Code, welche Sie vor dem Abgeben beheben müssen. Sie finden unten links am Rand im Reiter **"Problems"** eine Auflistung aller Syntaxfehler.


8. !!! error ""
    ```
    Note: \[...\] uses unsafe or unchecked operations.
    ```
    Dies ist nur eine Warnung und verhindert nicht die Abgabe der Hausübung. Sie sollten allerdings überprüfen, ob der entsprechende Abschnitt funktioniert.


9. !!! error  ""
    ```
    failed to delete some children.
    ```
    Dieser Fehler entsteht meistens dadurch, dass der Zugriff auf bestimmte Dateien durch andere Prozesse, wie z. B. den Debugger, blockiert wird. Ein Neustart von IntelliJ oder Ihrem Rechner sollte das Problem beheben.

10. !!! error ""
    ```
    Java.lang.OutOfMemoryError: java heap space
    ```
    Dieser Fehler kann manchmal beim Ausführen der Public Tests auftretten. Versuchen Sie zunächst die Public Tests erneut auszuführen oder IntelliJ neuzustarten. Falls der Fehler weiterhin auftritt, versuchen Sie [Java mehr Speicher zuzuweisen].

### Korrekte Java Version in IntelliJ einstellen

1. Überprüfen Sie zunächst in einem Terminal mit **"java --version"**, ob Java 17 benutzt wird (s. [Anleitung zum Installieren von Java])
2. Überprüfen Sie in IntelliJ, ob unter **"File" -> "Project Structure..." -> "Project" -> "SDK"** Java 17 als Version angegeben ist.
* Falls dies nicht der Fall ist, wählen Sie Java 17 aus und drücken Sie auf **"Apply"**.
3. Gehen Sie ebenfalls sicher, dass unter **"File" -> "Settings" -> "Build, Execution, Deployment" -> "Build Tools" -> "Gradle" -> "Gradle JVM"** als Option **"Project SDK"** ausgewählt ist.

### Java mehr Speicher zuweisen

1. Gehen Sie in Ihrem User Ordner in der Ordner **".gradle"**
* Unter Windows finden Sie den Ordner unter **"C:\Users\<UserName\>\\.gradle"** und auf Linux und Mac unter **"~/.gradle"**
2. Falls nicht vorhanden, erstellen Sie die Datei **"gradle.properties"**.
3. Fügen Sie in dieser Datei eine Zeile mit folgendem Eintrag hinzu:
```
org.gradle.jvmargs=-Xmx4096M
```
* Sie können auch versuchen die Zahl am Ende zu erhöhen, wenn der Fehler weiterhin auftritt.

!!! info "Information"
    Wenn Sie Ihr Problem nicht selber beheben konnten, können Sie entweder auf unserem Discord Server im Channel **"\#technical-issues"** oder im Moodle Forum für technische Fragen nachfragen. Fügen Sie bei beiden am besten einen Ausschnitt der Konsolenausgabe mit dem Fehler als Screenshot oder Text an.

## Hilfreich Fragen stellen

Beachten Sie die Seite [Bevor Sie eine Sprechstunde besuchen].

[Korrekte Java Version in IntelliJ Einstellen]: https://wiki.tudalgo.org/exercises/fix-errors/#korrekte-java-version-in-intellij-einstellen
[Anleitung zum Installieren von Java]: https://wiki.tudalgo.org/preparation/installation-java/
[Anleitung zum Exportieren]: https://wiki.tudalgo.org/exercises/export-upload/#exportieren
[Java mehr Speicher zuzuweisen]: https://wiki.tudalgo.org/exercises/fix-errors/#java-mehr-speicher-zuweisen
[Aktualisieren der Vorlage]: /exercises/download-import/#aktualisieren-der-vorlage
[Typische Programmierfehler]: /exercises/fix-errors/#typische-programmierfehler
[Bevor Sie eine Sprechstunde besuchen]: /support/good-bad-questions
[Debugging]: /exercises/fix-errors/#debugging