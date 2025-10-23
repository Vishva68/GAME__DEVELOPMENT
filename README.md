
## EX 5 : TWO DIMENSIONALTRANSFORMATION 


Name: Abhishek Kannan M
Reg no: 212224040007

**AIM**

To write a c program to implement 2D transformation of image.


**ALGORITHM**

Step 1:Start the program.

Step 2:Draw the image with default parameters.

Step 3 : Get the choice from the user.

Step 4: Get the parameters for transformation.

Step 5 : Perform the transformation.

Step 6 : Draw the image.

Step 7 : Stop the program.


**Program :**
```c
#include <graphics.h>
#include <stdio.h>
#include <conio.h>
#include <math.h>

void main()
{
    int gd = DETECT, gm, i, j, k, ch;
    float tx, ty, x, y, ang, n, temp;
    float a[5][3], si, co, b[5][3], c[5][3];

    initgraph(&gd, &gm, "c:\\turboc3\\bgi");
    n = 4;

    a[0][0] = 0;   a[0][1] = 0;
    a[1][0] = 100; a[1][1] = 0;
    a[2][0] = 100; a[2][1] = 100;
    a[3][0] = 0;   a[3][1] = 100;
    a[4][0] = 0;   a[4][1] = 0;

    while (1)
    {
        cleardevice();
        gotoxy(1, 8);

        printf("\n\t******** Program to perform 2-D Transformations ********");
        printf("\n\t\t\t 1. Accept the polygon");
        printf("\n\t\t\t 2. Perform translation");
        printf("\n\t\t\t 3. Perform scaling");
        printf("\n\t\t\t 4. Perform rotation");
        printf("\n\t\t\t 5. Perform reflection");
        printf("\n\t\t\t 6. Perform shearing");
        printf("\n\t\t\t 7. Exit");

        printf("\n\t\t\t Enter your choice::");
        scanf("%d", &ch);

        switch (ch)
        {
            case 1:
                cleardevice();
                gotoxy(1, 1);
                printf("\n\tEnter no of points.:");
                scanf("%f", &n);

                for (i = 0; i < n; i++)
                {
                    printf("\n\t Enter x,y co-ordinates for %d::", i + 1);
                    scanf("%f %f", &a[i][0], &a[i][1]);
                }
                a[i][0] = a[0][0];
                a[i][1] = a[0][1];

                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);
                getch();
                break;

            case 2:
                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);

                gotoxy(1, 1);
                printf("Enter translation vectors tx and ty\n\t");
                scanf("%f %f", &x, &y);

                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0] + x, 240 - (a[i][1] + y), 320 + a[i + 1][0] + x, 240 - (a[i + 1][1] + y));

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);
                getch();
                break;

            case 3:
                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);

                gotoxy(1, 1);
                printf("Enter scaling vectors tx and ty\n\t");
                scanf("%f %f", &x, &y);

                if (x == 0) x = 1;
                if (y == 0) y = 1;

                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + (a[i][0] * x), 240 - (a[i][1] * y), 320 + (a[i + 1][0] * x), 240 - (a[i + 1][1] * y));

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);
                getch();
                break;

            case 4:
                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);

                gotoxy(1, 1);
                printf("Enter the angle of rotation\n\t");
                scanf("%f", &ang);

                ang = ang * 0.01745;

                gotoxy(1, 3);
                printf("Enter point of rotation\n\t");
                scanf("%f %f", &x, &y);

                gotoxy(1, 5);
                printf("1.clockwise  2.anticlockwise\n\t");
                scanf("%d", &k);

                si = sin(ang);
                co = cos(ang);

                for (i = 0; i < n + 1; i++)
                {
                    c[i][0] = a[i][0];
                    c[i][1] = a[i][1];
                    c[i][2] = 1;
                }

                b[0][0] = co;    b[0][1] = si;    b[0][2] = 0;
                b[1][0] = -si;   b[1][1] = co;    b[1][2] = 0;
                b[2][0] = -x * co + (y * si) + x;
                b[2][1] = -x * si - (y * co) + y;
                b[2][2] = 1;

                if (k == 1)
                {
                    b[0][1] = -si;
                    b[1][0] = si;
                    b[2][0] = -x * co - (y * si) + x;
                    b[2][1] = -x * si + (y * co) + y;
                }

                for (i = 0; i < n + 1; i++)
                {
                    for (j = 0; j < 3; j++)
                    {
                        a[i][j] = 0;
                        for (k = 0; k < 3; k++)
                            a[i][j] = a[i][j] + c[i][k] * b[k][j];
                    }
                }

                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);
                getch();
                break;

            case 5:
                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);

                gotoxy(1, 1);
                printf("\n1.Reflection about Y-axis");
                printf("\n2.Reflection about X-axis");
                printf("\n3.Reflection about origin");
                printf("\n4.Reflection about line y=x");
                printf("\n5.Reflection about line y=-x");
                printf("\nEnter your choice:");
                scanf("%d", &ch);

                switch (ch)
                {
                    case 1:
                        for (i = 0; i < n + 1; i++)
                            a[i][0] = a[i][0] * -1;

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        getch();
                        break;

                    case 2:
                        for (i = 0; i < n + 1; i++)
                            a[i][1] = a[i][1] * -1;

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        getch();
                        break;

                    case 3:
                        for (i = 0; i < n + 1; i++)
                        {
                            a[i][1] = a[i][1] * -1;
                            a[i][0] = a[i][0] * -1;
                        }

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        getch();
                        break;

                    case 4:
                        for (i = 0; i < n + 1; i++)
                        {
                            temp = a[i][0];
                            a[i][0] = a[i][1];
                            a[i][1] = temp;
                        }

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        line(0, 479, 639, 0);
                        getch();
                        break;

                    case 5:
                        for (i = 0; i < n + 1; i++)
                        {
                            temp = a[i][0];
                            a[i][0] = a[i][1];
                            a[i][1] = temp;
                        }

                        for (i = 0; i < n + 1; i++)
                        {
                            a[i][1] = a[i][1] * -1;
                            a[i][0] = a[i][0] * -1;
                        }

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        line(0, 0, 639, 479);
                        getch();
                        break;

                    default:
                        break;
                }
                break;

            case 6:
                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);

                gotoxy(1, 1);
                printf("\n1.X shear with y reference line");
                printf("\n2.Y shear with x reference line");
                printf("\nEnter your choice:");
                scanf("%d", &ch);

                switch (ch)
                {
                    case 1:
                        printf("\nEnter the x-shear parameter value:");
                        scanf("%f", &temp);
                        printf("\nEnter the yref line");
                        scanf("%f", &ty);

                        b[0][0] = 1;       b[0][1] = 0;       b[0][2] = 0;
                        b[1][0] = temp;    b[1][1] = 1;       b[1][2] = 0;
                        b[2][0] = -temp * ty;
                        b[2][1] = 0;       b[2][2] = 1;

                        for (i = 0; i < n + 1; i++) a[i][2] = 1;

                        for (i = 0; i < n + 1; i++)
                        {
                            for (j = 0; j < 3; j++)
                            {
                                c[i][j] = 0;
                                for (k = 0; k < 3; k++)
                                    c[i][j] = c[i][j] + a[i][k] * b[k][j];
                            }
                        }

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + c[i][0], 240 - c[i][1], 320 + c[i + 1][0], 240 - c[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        getch();
                        break;

                    case 2:
                        printf("\nEnter the y-shear parameter value:");
                        scanf("%f", &temp);
                        printf("\nEnter the xref line");
                        scanf("%f", &tx);

                        b[0][0] = 1;       b[0][1] = temp;    b[0][2] = 0;
                        b[1][0] = 0;       b[1][1] = 1;       b[1][2] = 0;
                        b[2][0] = 0;       b[2][1] = -temp * tx; b[2][2] = 0;

                        for (i = 0; i < n + 1; i++) a[i][2] = 1;

                        for (i = 0; i < n + 1; i++)
                        {
                            for (j = 0; j < 3; j++)
                            {
                                c[i][j] = 0;
                                for (k = 0; k < 3; k++)
                                    c[i][j] = c[i][j] + a[i][k] * b[k][j];
                            }
                        }

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + c[i][0], 240 - c[i][1], 320 + c[i + 1][0], 240 - c[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        getch();
                        break;

                    default:
                        break;
                }
                break;

            case 7:
                exit(1);
                closegraph();
                restorecrtmode();
                break;

            default:
                break;
        }
    }
}


```


## Output :

**Polygon Dimensions**

<img width="632" height="442" alt="exp5_1" src="https://github.com/user-attachments/assets/96fa4f2c-18a0-4870-9fe2-9b6a78f15446" />

<img width="601" height="412" alt="exp5_2" src="https://github.com/user-attachments/assets/3e95c773-83f0-405a-9731-537c39d90a1b" />

<img width="627" height="468" alt="exp5_3" src="https://github.com/user-attachments/assets/24c8fad4-8231-433d-b338-5d54db23e2ce" />

---

**Translation**


<img width="632" height="442" alt="exp5_trans" src="https://github.com/user-attachments/assets/dbca2cf2-1d37-4ea3-881c-6b3e7e60ce9b" />

<img width="635" height="482" alt="exp5_4" src="https://github.com/user-attachments/assets/342440a0-5165-4bbd-b9bf-3ed634813504" />


<img width="631" height="458" alt="exp5_5" src="https://github.com/user-attachments/assets/560b4977-3c8d-4a3c-9ec4-9c61b4af8b69" />

---

**Scaling**

<img width="635" height="473" alt="exp5_scale" src="https://github.com/user-attachments/assets/311b426b-18fa-4f24-a37d-b8f0791bd509" />


<img width="638" height="473" alt="exp5_6" src="https://github.com/user-attachments/assets/be5d5c44-f4c3-4d2a-85dd-6763618ff09d" />


<img width="633" height="477" alt="exp5_7" src="https://github.com/user-attachments/assets/74f34a48-6f02-417a-a1d3-c36b9cab15d6" />

---

**Rotation**


<img width="635" height="468" alt="exp5_rot" src="https://github.com/user-attachments/assets/6a72f345-13e6-4de7-a411-0d6903926b54" />

**Clockwise**

<img width="636" height="482" alt="exp5_rot_cl_in" src="https://github.com/user-attachments/assets/e28d225d-c1eb-498e-bb44-70d3e9b74427" />

<img width="637" height="482" alt="exp5_rot_cl" src="https://github.com/user-attachments/assets/e85b5adb-0cb9-4142-877e-09eed229927d" />

**Anti-Clockwise**


<img width="637" height="478" alt="exp5_rot_ancl_in" src="https://github.com/user-attachments/assets/07c7292b-941f-4fbe-b450-2d14118766b0" />


<img width="637" height="471" alt="exp5_rot_ancl" src="https://github.com/user-attachments/assets/d738a6b2-cce4-413c-a0c8-7bf2a55fd3c3" />

---

**Reflection**


<img width="635" height="472" alt="exp5_ref" src="https://github.com/user-attachments/assets/3caa1578-e197-4aed-a0c5-32e86ed08cca" />

**Reflection about Y-axis**

<img width="638" height="476" alt="exp5_ref_1" src="https://github.com/user-attachments/assets/833708b4-ac20-4e6c-ad8d-bf29bc3af4e0" />


<img width="635" height="478" alt="exp5_ref_1_1" src="https://github.com/user-attachments/assets/e98d0a90-4cb7-40c9-8478-4c2e5a815bb7" />


**Reflection about X-axis**


<img width="641" height="482" alt="exp5_ref_2" src="https://github.com/user-attachments/assets/6ec67745-4abc-43c1-a7ae-267757876a8f" />


<img width="642" height="478" alt="exp5_ref_2_1" src="https://github.com/user-attachments/assets/94cf068f-9234-49f6-8417-08a463fe7682" />



**Reflection about Origin**


<img width="638" height="466" alt="exp5_ref_3" src="https://github.com/user-attachments/assets/91ceed57-2d3c-49d5-a808-b039321558a7" />



<img width="637" height="477" alt="exp5_ref_3_1" src="https://github.com/user-attachments/assets/86bbbbbe-9990-45b6-ba52-f587ea48df6c" />


**Reflection about line y=x**

<img width="638" height="476" alt="exp5_ref_4" src="https://github.com/user-attachments/assets/0b023dbe-eb9c-4779-a150-a07a93d20be0" />


<img width="638" height="477" alt="exp5_ref_4_1" src="https://github.com/user-attachments/assets/7c4cce99-884f-4761-8538-e0ec6f609508" />


**Reflection about line y=-x**

<img width="642" height="476" alt="exp5_ref_5" src="https://github.com/user-attachments/assets/34b1ce93-94d7-41c2-a840-2f3d7c956821" />


<img width="633" height="473" alt="exp5_ref_5_1" src="https://github.com/user-attachments/assets/95ca0243-a708-4b9e-81d0-82849e8bf6ea" />


---

**Shearing**


<img width="638" height="480" alt="exp5_shear" src="https://github.com/user-attachments/assets/db9b3241-598f-407b-a248-604bce546289" />


**X Shear with y reference line**


<img width="638" height="476" alt="exp5_shear_1" src="https://github.com/user-attachments/assets/3cf0c5fb-3769-42df-9e33-b44f61968170" />


<img width="635" height="472" alt="exp5_shear_1_1" src="https://github.com/user-attachments/assets/20d816c8-803c-4f58-9d0f-bddaaa8da7b4" />



**Y Shear with x reference line**


<img width="641" height="473" alt="exp5_shear_2" src="https://github.com/user-attachments/assets/1f82d463-ced3-4bb3-91b0-b206a2ba4df9" />



<img width="636" height="470" alt="exp5_shear_2_1" src="https://github.com/user-attachments/assets/39c39f5d-b966-4f1c-aed5-67c0cf1baa03" />



---


## Result :

Thus, the program was Completed and the output was obtained successfully.
