# movingImage

Для решения этой задачи, вы можете использовать JavaFX, который позволяет создавать графические интерфейсы и анимации. Ниже приведен код, который демонстрирует движение изображения из левого верхнего угла в правый нижний угол на квадратной панели. Когда изображение скрывается за пределами экрана, оно будет появляться снова из верхнего левого угла.
```java
import javafx.animation.KeyFrame;
import javafx.animation.Timeline;
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.image.Image;
import javafx.scene.image.ImageView;
import javafx.scene.layout.Pane;
import javafx.scene.paint.Color;
import javafx.scene.shape.Rectangle;
import javafx.util.Duration;
import java.io.File;

public class MovingImage extends Application {

    private final double PANEL_WIDTH = 400;
    private final double PANEL_HEIGHT = 400;
    private final double IMAGE_WIDTH = 100;
    private final double IMAGE_HEIGHT = 100;
    private final String IMAGE_PATH = "image.png";

    @Override
    public void start(java.awt.EventObject event) {
        Pane root = new Pane();
        root.setStyle("-fx-background-color: #FFFFFF;");

        Image image = new Image(new File(IMAGE_PATH).toURI().toString());
        ImageView imageView = new ImageView(image);
        imageView.setFitHeight(IMAGE_HEIGHT);
        imageView.setFitWidth(IMAGE_WIDTH);

        Rectangle panel = new Rectangle(PANEL_WIDTH, PANEL_HEIGHT, Color.TRANSPARENT);
        root.getChildren().addAll(panel, imageView);

        Timeline timeline = new Timeline(new KeyFrame(Duration.seconds(1), e -> {
            imageView.setLayoutX(imageView.getLayoutX() + 5);
            if (imageView.getLayoutX() > panel.getWidth() - imageView.getWidth()) {
                imageView.setLayoutX(0);
                imageView.setLayoutY(imageView.getLayoutY() + 5);
                if (imageView.getLayoutY() > panel.getHeight() - imageView.getHeight()) {
                    imageView.setLayoutY(0);
                }
            }
        }));
        timeline.setCycleCount(Timeline.INDEFINITE);
        timeline.play();

        Scene scene = new Scene(root, PANEL_WIDTH, PANEL_HEIGHT);

        launch(scene);
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```
Сохраните этот код в файле `MovingImage.java` и замените `image.png` на путь к вашему изображению. Затем вы можете запустить программу, и изображение будет двигаться по квадратной панели, появляясь снова, когда оно скрывается за пределами экрана.
