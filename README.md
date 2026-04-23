//Student Attendence Tracker using C.

#include <stdio.h>
#include <string.h>

#define MAX 100

struct Student {
    int roll;
    char name[50];
    int totalClasses;
    int attended;
};

struct Student s[MAX];
int count = 0;

// Add Student
void addStudent() {
    printf("\nEnter Roll Number: ");
    scanf("%d", &s[count].roll);

    printf("Enter Name: ");
    scanf(" %[^\n]", s[count].name);

    s[count].totalClasses = 0;
    s[count].attended = 0;

    count++;
    printf("✅ Student Added Successfully!\n");
}

// Display Students
void displayStudents() {
    printf("\n--- Student List ---\n");
    for(int i = 0; i < count; i++) {
        printf("Roll: %d | Name: %s\n", s[i].roll, s[i].name);
    }
}

// Mark Attendance
void markAttendance() {
    int roll, found = 0;
    printf("\nEnter Roll Number: ");
    scanf("%d", &roll);

    for(int i = 0; i < count; i++) {
        if(s[i].roll == roll) {
            found = 1;
            s[i].totalClasses++;

            int present;
            printf("Present? (1 = Yes, 0 = No): ");
            scanf("%d", &present);

            if(present == 1)
                s[i].attended++;

            printf("✅ Attendance Marked!\n");
        }
    }

    if(!found)
        printf("❌ Student Not Found!\n");
}

// View Attendance
void viewAttendance() {
    printf("\n--- Attendance Report ---\n");
    for(int i = 0; i < count; i++) {
        float percentage = 0;
        if(s[i].totalClasses > 0)
            percentage = (float)s[i].attended / s[i].totalClasses * 100;

        printf("Roll: %d | Name: %s | Attendance: %.2f%%\n",
               s[i].roll, s[i].name, percentage);
    }
}

// Search Student
void searchStudent() {
    int roll, found = 0;
    printf("\nEnter Roll Number: ");
    scanf("%d", &roll);

    for(int i = 0; i < count; i++) {
        if(s[i].roll == roll) {
            found = 1;
            printf("Found: %s\n", s[i].name);
        }
    }

    if(!found)
        printf("❌ Student Not Found!\n");
}

int main() {
    int choice;

    while(1) {
        printf("\n\n===== Student Attendance Tracker =====\n");
        printf("1. Add Student\n");
        printf("2. Display Students\n");
        printf("3. Mark Attendance\n");
        printf("4. View Attendance\n");
        printf("5. Search Student\n");
        printf("6. Exit\n");

        printf("Enter Choice: ");
        scanf("%d", &choice);

        switch(choice) {
            case 1: addStudent(); break;
            case 2: displayStudents(); break;
            case 3: markAttendance(); break;
            case 4: viewAttendance(); break;
            case 5: searchStudent(); break;
            case 6: return 0;
            default: printf("Invalid Choice!\n");
        }
    }
}
