### Adapter Pattern Documentation

---

#### Overview

The Adapter pattern is a structural design pattern that enables the collaboration between classes with incompatible interfaces. It acts as a bridge between two incompatible interfaces by converting the interface of one class into another interface that a client expects. This pattern is useful when integrating legacy code with new systems or when working with third-party libraries with incompatible interfaces.

---

#### Key Components

1. **Target Interface:** Defines the interface that the client expects.

2. **Adaptee:** Represents the existing class with an incompatible interface that needs to be adapted.

3. **Adapter:** Implements the Target interface and wraps the Adaptee, providing a compatible interface to the client.

---

#### Example Scenario

Consider an example scenario of adapting a legacy audio player with a new media player interface.

##### Step 1: Define the Target Interface

```java
// Target Interface
public interface MediaPlayer {
    void play(String mediaType, String fileName);
}
```

##### Step 2: Implement the Adaptee (Legacy Audio Player)

```java
// Adaptee (Legacy Audio Player)
public class AudioPlayer {
    public void playAudio(String fileName) {
        System.out.println("Playing audio file: " + fileName);
    }
}
```

##### Step 3: Implement the Adapter

```java
// Adapter
public class AudioPlayerAdapter implements MediaPlayer {
    private AudioPlayer audioPlayer;

    public AudioPlayerAdapter() {
        this.audioPlayer = new AudioPlayer();
    }

    @Override
    public void play(String mediaType, String fileName) {
        if (mediaType.equalsIgnoreCase("mp3")) {
            audioPlayer.playAudio(fileName);
        } else if (mediaType.equalsIgnoreCase("mp4") || mediaType.equalsIgnoreCase("vlc")) {
            System.out.println("Unsupported media type: " + mediaType);
        } else {
            System.out.println("Invalid media type: " + mediaType);
        }
    }
}
```

##### Step 4: Use the Adapter in Client Code

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        MediaPlayer player = new AudioPlayerAdapter();

        player.play("mp3", "song.mp3");
        player.play("mp4", "video.mp4");
    }
}
```

---

#### Summary

The Adapter pattern facilitates the integration between classes with incompatible interfaces, promoting reusability and interoperability. It enables legacy code to work seamlessly with new systems and allows the use of third-party libraries with different interfaces. By providing a consistent interface to the client, the Adapter pattern simplifies the interaction between components in a system.
