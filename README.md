import controlP5.*;

ControlP5 cp5;

int num = 50;
int threshold = 100;
boolean showCircles = true;

Circle c1;
ArrayList<Circle> particles = new ArrayList<Circle>();



void setup() {
  size(800, 500);
  background(255);



  for (int i = 0; i < num; i++) {
    c1 = new Circle();
    particles.add(c1);
  }

  // slider
  cp5 = new ControlP5(this);
 
  cp5.addSlider("threshold")
    .setPosition(20, 20)
    .setRange(0, 1000); 
}



void draw() {
  background(10, 20, 30);

  for (int i = 0; i < num; i++) {

    for (int j = 0; j < num; j++) {
      if (i != j) {
        float dist = dist(particles.get(i).pos.x, particles.get(i).pos.y, particles.get(j).pos.x, particles.get(j).pos.y );

        if (dist < threshold) {
          float alpha = map(dist, 0, threshold, 255, 0);
          stroke(120, 254, 207, alpha);
          line(particles.get(i).pos.x, particles.get(i).pos.y, particles.get(j).pos.x, particles.get(j).pos.y);
        }
      }
    }
    
    particles.get(i).updateCircle();
    particles.get(i).drawCircle();
  }
}
