/**
     An age reader that I started to make, then @Element118 finished it for me.
    Credit to @ChesterBanks for the background.
    
    If its not right then restart and try again
*/
textFont(createFont("Impact"));
var answer = 0;
var clicked = false;
mouseClicked = function() {
    clicked = true;
};
var page = "start";
var a = 255;

var button = function(string, x, y, w, h, nextPage) {
    fill(255, 255, 255, 200+sin((frameCount+x*5)*5)*50);
    rect(x, y, w, h);
    textAlign(CENTER, CENTER);
    fill(0, 47, 64, 200+sin((frameCount+x*5)*5)*50);
    text(string, x+w/2, y+h/2);
    if (mouseX > x && mouseY > y && mouseX < x+w && mouseY < y+h && a > 250) {
        cursor(HAND);
        if (clicked) {
            if (string === "Yes") {
                answer += 1<<page;
            }
            mouseX = 0;
            page = nextPage;
            a = 1;
        }
    }
};

var back = function() {
    noStroke();
    background(0, 47, 64);
    for(var i = 0; i < 360; i += 24){
        for(var j = 0; j < 360; j += 46){
            pushMatrix();
            noStroke();
            translate(200, 200);
            rotate(frameCount/20 * 20);
            rotate(i);
            fill(0, 187, 255, -j + 200);
            arc(0, 35 + j, 100 + sin(frameCount * 10) * 5, 77 + sin(frameCount * 10) * 5, -110, 0);
            popMatrix();
        }
    }
};

draw = function() {
    cursor(ARROW);
    if (page === "start") {
        back();
        
        textAlign(CENTER, CENTER);
        textSize(60);
        fill(255, 255, 255, 150);
        text("AGE READER", 200, 140);
        text("AGE READER", 200, 143);
        
        textSize(20);
        text("(just press yes or no)", 200, 188);
        text("(just press yes or no)", 200, 190);
        
        button("Start", 150, 270, 100, 50, 0);
    }
    if (0 <= page && page <= 6) {
        back();
        
        var numbers = [];
        for (var i=1;i<=100;i++) {
            if (i&(1<<page)) {
                numbers.push(i);
            }
        }
        
        textAlign(LEFT, TOP);
        textSize(25);
        fill(255, 255, 255, 150);
        text(numbers.join(" "), 10, 10, 390, 200);
        text(numbers.join(" "), 10, 11, 390, 200);
        textAlign(CENTER, CENTER);
        text("Is your age in these numbers?", 200, 200);
        text("Is your age in these numbers?", 200, 201);
        
        textSize(20);
        button("Yes", 75, 300, 100, 50, page===6?"done":page+1);
        button("No", 225, 300, 100, 50, page===6?"done":page+1);
    }
    if (page === 'done') {
        back();
        
        textAlign(CENTER, CENTER);
        textSize(30);
        fill(255, 255, 255, 150);
        text("Your age is", 200, 150);
        text("Your age is", 200, 152);
        
        textSize(130);
        text(answer, 200, 240);
        text(answer, 200, 243);
    }
    
    fill(255, 255, 255, 255-a);
    rect(0, 0, 400, 400);
    if (a < 255) {
        a *= 1.2;
    }
    clicked = false;
};
