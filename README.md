#include<windows.h>
#ifdef __APPLE__
#include <GLUT/glut.h>
#else
#include <GL/glut.h>
#endif
#include <stdlib.h>
#include <math.h>

float xrot = 0.0;
float yrot = 0.0;
float xdiff = 0.0;
float ydiff = 0.0;
bool mouseDown = false;
int is_depth;
static GLfloat spin = 0.0;
static GLfloat spin_speed = 1.0;
//int x1=5,y1=-15,z1=10,z2=10;
void init(void);
void tampil(void);
void keyboard(unsigned char, int, int);
void ukuran (int, int);

void keyboard (unsigned char key, int x, int y){
    switch (key)
    {
        //GESER KE KIRI
    case 'a':
        glTranslatef(-3.0, 0.0, 0.0);
        break;
    case 'A':
        glTranslatef(-1.0, 0.0, 0.0);
        break;
        //GESER KE KANAN
    case 'd':
        glTranslatef(3.0, 0.0, 0.0);
        break;
    case 'D':
        glTranslatef(2.0, 0.0, 0.0);
        break;
        //GESER KE ATAS
    case '7':
        glTranslatef(0.0, 1.5, 0.0);
        break;

    case '9':
        glTranslatef(0.0, -1.5f, 0.0);
        break;

        //GERAK KE DEPAN
    case 'w':
        glTranslatef(0.0, 0.0, 3.0f);
        break;
    case 'W':
        glTranslatef(0.0, 0.0, 5.5);
        break;
        //GERAK KE BELAKANG
    case 's':
        glTranslatef(0.0, 0.0, -1.5f);
        break;
    case 'S':
        glTranslatef(0.0, 0.0, -3.5f);
        break;
        //ROTATE KE KIRI
    case '4':
        glRotatef(1.0, 0.0, -5.0, 0.0);
        break;
    case 'K':
        glRotatef(5.0, 0.0, -5.0, 0.0);
        break;
        //ROTATE KE KANAN
    case '6':
        glRotatef(1.0, 0.0, 5.0, 0.0);
        break;
    case '/':
        glRotatef(2.0, 0.0, 5.0, 0.0);
        break;

    case '5':
        if(is_depth){
            is_depth=0;
            glDisable(GL_DEPTH_TEST);
        }
        else{
            is_depth=1;
            glEnable(GL_DEPTH_TEST);
        }
        break;
		case '3':
			glRotatef(1.0, 0.0, 0.0, -5.0);
			break;
			//rotate ke samping kiri
		case '1':
			glRotatef(1.0, 0.0, 0.0, 5.0);
			break;
		case 'i':
			glRotatef(5.0, 0.0, 0.0, 5.0);
			break;
			//rotate ke atas
		case '8':
			glRotatef(1.0, -5.0, 0.0, 0.0);
			break;
		case 'u':
			glRotatef(5.0, -5.0, 0.0, 0.0);
			break;
			//rotate ke bawah
		case '2':
			glRotatef(1.0, 5.0, 0.0, 0.0);
			break;
		case 'l':
			glRotatef(5.0, 5.0, 0.0, 0.0);
			break;
    }
    tampil();
}
void mouse(int button, int state, int x, int y){
    if(button == GLUT_LEFT_BUTTON && state == GLUT_DOWN){
        mouseDown = true;
        xdiff = x-yrot;
        ydiff = -y + xrot;
    }else{
        mouseDown = false;
    }
    glutPostRedisplay();
}
void mouseMotion(int x, int y){
    if(mouseDown){
        yrot = x - xdiff;
        xrot = y + ydiff;
        glutPostRedisplay();
    }
}
int main(int argc, char **argv){
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_DOUBLE|GLUT_RGB);
    glutInitWindowSize(800,600);
    glutInitWindowPosition(250,80);
    glutCreateWindow("Eliansion Ivan-672018311");
    init();
    glutDisplayFunc(tampil);
    glutKeyboardFunc(keyboard);
    glutMouseFunc(mouse);
    glutMotionFunc(mouseMotion);
    glutReshapeFunc(ukuran);
    glutMainLoop();
    return 0;
}
void init(void){
    glClearColor(0.0,0.0,0.0,0.0);
    glEnable(GL_DEPTH_TEST);
    is_depth=1;
    glMatrixMode(GL_MODELVIEW);
    glPointSize(9.0);
    glLineWidth(6.0f);
}
void pilar_nyabang_mario(){
    //pilar 1 nyabang kiri
    //depan
    glColor3ub(200, 150, 120);
    glVertex3f(-21.5,8,10);
    glVertex3f(-25,8,12);
    glVertex3f(-25,-12,12);
    glVertex3f(-21.5,-12,10);

    //belakang
    glVertex3f(-23,8,5.5);
    glVertex3f(-26.5,8,7.5);
    glVertex3f(-26.5,-12,7.5);
    glVertex3f(-23,-12,5);

    //kiri
    glVertex3f(-26.5,8,7.5);
    glVertex3f(-26.5,-12,7.5);
    glVertex3f(-25,-12,12);
    glVertex3f(-25,8,12);

    //kanan
    glVertex3f(-22,8,10);
    glVertex3f(-22,-12,10);
    glVertex3f(-23,-12,6);
    glVertex3f(-23,8,6);


    //atas
    glVertex3f(-21.5,8,10);
    glVertex3f(-25,8,12);
    glVertex3f(-26.5,8,7.5);
    glVertex3f(-23,8,5.5);




    //pilar 2 nyabang kiri
    //glColor3f(0,1,0);
    glVertex3f(-23,8,5.5);
    glVertex3f(-26.5,8,3.5);
    glVertex3f(-26.5,-12,3.5);
    glVertex3f(-23,-12,5);

    glVertex3f(-21.5,8,0);
    glVertex3f(-25,8,-2);
    glVertex3f(-25,-12,-2);
    glVertex3f(-21.5,-12,0);

    glVertex3f(-26.5,8,3.5);
    glVertex3f(-26.5,-12,3.5);
    glVertex3f(-25,-12,-2);
    glVertex3f(-25,8,-2);

    glVertex3f(-22,8,0);
    glVertex3f(-22,-12,0);
    glVertex3f(-23,-12,5);
    glVertex3f(-23,8,5);

    //atasnya
    glVertex3f(-21.5,8,0);
    glVertex3f(-25,8,-2);
    glVertex3f(-26.5,8,3.5);
    glVertex3f(-23,8,5.5);
}
void segitiga(){
    // kerucut nya kiri
    glColor3f(0.8,0.2,0.2);
    glBegin(GL_TRIANGLES);
    glVertex3f(-21.5,8,10);
    glVertex3f(-25,8,12);
    glVertex3f(-24,13,9);

    glVertex3f(-25,8,12);
    glVertex3f(-26.5,8,7.5);
    glVertex3f(-24,13,9);

    glVertex3f(-26.5,8,7.5);
    glVertex3f(-23,8,5.5);
    glVertex3f(-24,13,9);

    glVertex3f(-21.5,8,10);
    glVertex3f(-23,8,5.5);
    glVertex3f(-24,13,9);

    //kerucut kanan
    glColor3f(0.8,0.2,0.2);
    glBegin(GL_TRIANGLES);
    glVertex3f(21.5,8,10);
    glVertex3f(25,8,12);
    glVertex3f(24,13,9);

    glVertex3f(25,8,12);
    glVertex3f(26.5,8,7.5);
    glVertex3f(24,13,9);

    glVertex3f(26.5,8,7.5);
    glVertex3f(23,8,5.5);
    glVertex3f(24,13,9);

    glVertex3f(21.5,8,10);
    glVertex3f(23,8,5.5);
    glVertex3f(24,13,9);

    //kerucut belakang
    glVertex3f(-21.5,8,0);
    glVertex3f(-25,8,-2);
    glVertex3f(-24,14,1);

    glVertex3f(-25,8,-2);
    glVertex3f(-26.5,8,3.5);
    glVertex3f(-24,14,1);

    glVertex3f(-26.5,8,3.5);
    glVertex3f(-23,8,5.5);
    glVertex3f(-24,14,1);

     glVertex3f(-21.5,8,0);
     glVertex3f(-23,8,5.5);
     glVertex3f(-24,14,1);

         //kerucut belakang kanan
    glVertex3f(21.5,8,0);
    glVertex3f(25,8,-2);
    glVertex3f(24,14,1);

    glVertex3f(25,8,-2);
    glVertex3f(26.5,8,3.5);
    glVertex3f(24,14,1);

    glVertex3f(26.5,8,3.5);
    glVertex3f(23,8,5.5);
    glVertex3f(24,14,1);

     glVertex3f(21.5,8,0);
     glVertex3f(23,8,5.5);
     glVertex3f(24,14,1);

     //yang bagian pilar

    glVertex3f(-6,12,11);
    glVertex3f(-11,12,11);
    glVertex3f(-8.5,19,5);

    glVertex3f(-11,12,11);
    glVertex3f(-11,12,-1);
    glVertex3f(-8.5,19,5);

    glVertex3f(-6,12,11);
    glVertex3f(-6,12,-1);
    glVertex3f(-8.5,19,5);

    glVertex3f(-11,12,-1);
    glVertex3f(-6,12,-1);
    glVertex3f(-8.5,19,5);

    //yang kanan
    glVertex3f(6,12,11);
    glVertex3f(11,12,11);
    glVertex3f(8.5,19,5);

    glVertex3f(11,12,11);
    glVertex3f(11,12,-1);
    glVertex3f(8.5,19,5);

    glVertex3f(6,12,11);
    glVertex3f(6,12,-1);
    glVertex3f(8.5,19,5);

    glVertex3f(11,12,-1);
    glVertex3f(6,12,-1);
    glVertex3f(8.5,19,5);

    //yang kerucut kecil unyu2 belakang
    glVertex3f(37,0,-7);
    glVertex3f(34,0,-6);
    glVertex3f(36,4,-8.5);

    glVertex3f(34,0,-6);
    glVertex3f(34,0,-9);
    glVertex3f(36,4,-8.5);

     glVertex3f(37,0,-7);
     glVertex3f(37,0,-10);
     glVertex3f(36,4,-8.5);

    glVertex3f(34,0,-9);
    glVertex3f(37,0,-10);
    glVertex3f(36,4,-8.5);

        //yang kerucut kecil unyu2 belakang
    glVertex3f(-37,0,-7);
    glVertex3f(-34,0,-6);
    glVertex3f(-36,4,-8.5);

    glVertex3f(-34,0,-6);
    glVertex3f(-34,0,-9);
    glVertex3f(-36,4,-8.5);

     glVertex3f(-37,0,-7);
     glVertex3f(-37,0,-10);
     glVertex3f(-36,4,-8.5);

    glVertex3f(-34,0,-9);
    glVertex3f(-37,0,-10);
    glVertex3f(-36,4,-8.5);

    //yang kerucut unyu kanan
    glVertex3f(29,0,19);
    glVertex3f(29,0,25);
    glVertex3f(30,4,23);


    glVertex3f(29,0,25);
    glVertex3f(31,0,25);
    glVertex3f(30,4,23);

    glVertex3f(29,0,21);
    glVertex3f(31,0,21);
    glVertex3f(30,4,23);

    glVertex3f(31,0,21);
    glVertex3f(31,0,25);
    glVertex3f(30,4,23);

        //yang kerucut unyu
    glVertex3f(-29,0,19);
    glVertex3f(-29,0,25);
    glVertex3f(-30,4,23);


    glVertex3f(-29,0,25);
    glVertex3f(-31,0,25);
    glVertex3f(-30,4,23);

    glVertex3f(-29,0,21);
    glVertex3f(-31,0,21);
    glVertex3f(-30,4,23);

    glVertex3f(-31,0,21);
    glVertex3f(-31,0,25);
    glVertex3f(-30,4,23);

    //yang kerucut
    glVertex3f(30,0,-10);
    glVertex3f(28,0,-10);
    glVertex3f(29,4,-13);

    glVertex3f(28,0,-10);
    glVertex3f(28,0,-14);
    glVertex3f(29,4,-13);

    glVertex3f(30,0,-10);
    glVertex3f(30,0,-14);
    glVertex3f(29,4,-13);

    glVertex3f(28,0,-14);
    glVertex3f(30,0,-14);
    glVertex3f(29,4,-13);

    //kiri
    glVertex3f(-30,0,-10);
    glVertex3f(-28,0,-10);
    glVertex3f(-29,4,-13);

    glVertex3f(-28,0,-10);
    glVertex3f(-28,0,-14);
    glVertex3f(-29,4,-13);

    glVertex3f(-30,0,-10);
    glVertex3f(-30,0,-14);
    glVertex3f(-29,4,-13);

    glVertex3f(-28,0,-14);
    glVertex3f(-30,0,-14);
    glVertex3f(-29,4,-13);


    //kerucut depan
    glVertex3f(37,0,17);//udah
    glVertex3f(34,0,16);
    glVertex3f(36,4,18);

    glVertex3f(34,0,16);
    glVertex3f(34,0,19);
    glVertex3f(36,4,18);

    glVertex3f(37,0,17);
    glVertex3f(37,0,20);
    glVertex3f(36,4,18);

    glVertex3f(34,0,19);
    glVertex3f(37,0,20);
    glVertex3f(36,4,18);

    //kerucut depan kiri
    glVertex3f(-37,0,17);//udah
    glVertex3f(-34,0,16);
    glVertex3f(-36,4,18);

    glVertex3f(-34,0,16);
    glVertex3f(-34,0,19);
    glVertex3f(-36,4,18);

    glVertex3f(-37,0,17);
    glVertex3f(-37,0,20);
    glVertex3f(-36,4,18);

    glVertex3f(-34,0,19);
    glVertex3f(-37,0,20);
    glVertex3f(-36,4,18);

    glEnd();

}

void kotak_depan_cabang(){
    glColor3ub(237, 194, 183);
    //kiri
    glVertex3f(-26, 3, 2);
    glVertex3f(-26, -12, 2);
    glVertex3f(-26, -12, 8);
    glVertex3f(-26, 3, 8);

    //belakang
    glVertex3f(-28, 3, 2);
    glVertex3f(-28, -12, 2);
    glVertex3f(-22, -12, 2);
    glVertex3f(-22, 3,2);

    //depan
    glVertex3f(-28, 3, 8);
    glVertex3f(-28, -12, 8);
    glVertex3f(-22, -12, 8);
    glVertex3f(-22, 3, 8);

    //atas
    glVertex3f(-28, 3, 2);
    glVertex3f(-28, 3, 8);
    glVertex3f(-23, 3, 8);
    glVertex3f(-23, 3, 2);

}
void dua_kali_cabang(){

  glColor3ub(237, 194, 183);
  //kiri
    glVertex3f(-30,2,8);
    glVertex3f(-30,2,2);
    glVertex3f(-30,-12,2);
    glVertex3f(-30,-12,8);

//    kanan
    glVertex3f(-25,2,12);
    glVertex3f(-25,2,-1);
    glVertex3f(-25,-12,-1);
    glVertex3f(-25,-12,12);


//depan belakang boleh apus
    //depan
    glVertex3f(-30,2,8);
    glVertex3f(-25,2,8);
    glVertex3f(-25,-12,8);
    glVertex3f(-30,-12,8);

    //belakang
    glVertex3f(-30,2,2);
    glVertex3f(-25,2,2);
    glVertex3f(-25,-12,2);
    glVertex3f(-30,-12,2);

    //atas
    glVertex3f(-30, 2, 2);
    glVertex3f(-30, 2, 8);
    glVertex3f(-25, 2, 8);
    glVertex3f(-25, 2, 2);

    //mau nyabang lagi ijo
    //depan
    //glColor3f(0.2,1.3,2.1);
    glVertex3f(-30,2,8);//a
    glVertex3f(-25,2,12);//b
    glVertex3f(-25,-12,12);//c
    glVertex3f(-30,-12,8);//d

    //belakang nya
    //glColor3f(0.2,1.3,2.1);
    glVertex3f(-30,-12,2);
    glVertex3f(-30,2,2);
    glVertex3f(-25,2,-2);//b
    glVertex3f(-25,-12,-2);

    //depannya kanan
    //glColor3f(0.3,1.2,0.2);
    glVertex3f(-25,1,12);//b
    glVertex3f(-25,-12,12);//c
    glVertex3f(-30,-12,22);//c
    glVertex3f(-30,1,22);//b

    //depannya kiri
    //glColor3f(0.3,1.2,0.2);
    glVertex3f(-30,1,8);//b
    glVertex3f(-30,-12,8);//c
    glVertex3f(-35,-12,18);//c
    glVertex3f(-35,1,18);

    //depan
    //glColor3f(0.5,0.5,0.5);
    glVertex3f(-30,-12,22);//c
    glVertex3f(-30,1,22);
    glVertex3f(-35,1,18);
    glVertex3f(-35,-12,18);//c

    //atas ijo
    glVertex3f(-30,1,22);
    glVertex3f(-35,1,18);
    glVertex3f(-30,1,8);//a
    glVertex3f(-25,1,12);//

    //kotak belkang kiri
    //glColor3f(0.3,0.5,0.2);
    glVertex3f(-30,1,2);//b
    glVertex3f(-30,-12,2);//c
    glVertex3f(-35,-12,-8);//c
    glVertex3f(-35,1,-8);

    //kotak belakang kanan
    glVertex3f(-25,1,-2);//b
    glVertex3f(-25,-12,-2);//c
    glVertex3f(-29,-12,-12);//c
    glVertex3f(-29,1,-12);

    //atas
        glVertex3f(-30,1,2);//b
        glVertex3f(-35,1,-8);
        glVertex3f(-29,1,-12);
        glVertex3f(-25,1,-2);//b



        //tutup belakang
        glVertex3f(-35,1,-8);
        glVertex3f(-29,1,-12);
        glVertex3f(-29,-12,-12);
        glVertex3f(-35,-12,-8);
//
//
//    //kotak didalam depan
//        glColor3f(0.5,0.5,0.9);
//        //depan
//    glVertex3f(-31,-12,26);//c
//    glVertex3f(-31,1,26);
//    glVertex3f(-35,1,24);
//    glVertex3f(-35,-12,24);
//
//    //belakang nya
//    glColor3f(0.5,0.5,0.9);
//    glVertex3f(-30,-12,22);//c
//    glVertex3f(-30,1,22);
//    glVertex3f(-32,1,20);
//    glVertex3f(-32,-12,20);
//
//    //kanan
//    glVertex3f(-34,1,21);
//    glVertex3f(-34,-12,21);
//    glVertex3f(-32,-12,18);
//    glVertex3f(-32,1,18);
//
//    //kiri
//    glVertex3f(-30,1,20);
//    glVertex3f(-30,-12,20);
//    glVertex3f(-32,-12,23);//c
//    glVertex3f(-32,1,23);
//
//    //atas
//    glVertex3f(-32,1,23);
//    glVertex3f(-34,1,21);
//    glVertex3f(-32,1,18);
//    glVertex3f(-30,1,20);
//



}
