# CLI-Based-Networking-Application
# Student Networking CLI Application

## Program Scenario

The **Student Networking CLI Application** is a text-based platform designed for students in the School of Computer Science to connect with each other, communicate, and collaborate. This application mimics a social media environment made specifically for students, allowing them to create profiles, send and receive messages, manage study groups, add friends, and track their activities.

Built using object-oriented programming principles in **C++**, the application makes use of various abstract data types (ADTs) including **Doubly Linked Lists**, **Queues**, **Stacks**, and **Circular Linked Lists** to ensure efficient data management and user interaction. It also makes use of various other concepts like `try-catch` error handling, templates, etc.

---

## Core Functionalities

### 1. Profile Management
- Users can create, view, and manage student profiles using a Doubly Linked List.
- View all profiles or browse one by one.
- Option to delete their own profile.

### 2. Messaging System
- A Queue is used to manage messages sent and received by students.
- Implemented using the `Message` ADT containing timestamp, content, and pointer to the next message.

### 3. Action History
- A Stack is used to track recent actions like `CREATE_PROFILE`, `ADD_FRIEND`, and `SEND_MESSAGE` using the `UndoableAction` class.
- All actions share the same stack and can be undone in LIFO order.

### 4. Study Group Management
- A Circular Linked List groups students by shared courses.
- New groups are created dynamically when a new course is entered.

### 5. Friend List Management
- Users can send friend requests, accept them, and manage friend lists.
- Connections are managed using pointer-to-pointer relationships.
- Undoing friend actions updates both friend lists.

---

## Program Analysis

### Program Requirements

#### Functional Requirements

**Student Profile Management**
- Create new student profiles with name, course, and matric number
- View profiles in forward/backward order or one-by-one

**Friends Management**
- Send, view, and accept friend requests
- View current friend list

**Messaging System**
- Send messages to friends
- View inbox and full message threads

**Action History**
- Undo last action (profile creation, friend addition, or message sending)

**Study Group Management**
- Group students by course
- View and rotate through group members

#### Technical Specifications
- **Language:** C++
- **OOP Principles** and **manual memory management** (no STL)
- Uses multiple files for clarity
- Exception handling using `try/catch`
- Template classes implemented

**Data Structures:**
- **Doubly Linked List:** Student profiles
- **Queue:** Message inbox
- **Stack:** Undo feature
- **Circular Linked List:** Study groups

#### Non-Functional Requirements

**Usability**
- CLI menu with user login/logout functionality

**Error Handling**
- Input validation with error prompts
- Exceptions handled via `try-catch` to ensure smooth UX

---

## Constraints, Limitations, and Challenges

### Constraints
- No real networking (simulated offline)
- No persistence (data lost on exit)
- Single-user login only

### Limitations

**Hardware**
- Works on any standard CPU architecture
- Requires basic I/O devices (keyboard + monitor)

**Software**
- Cross-platform support (Windows, Linux, macOS)
- Requires C++ compiler (GCC, Clang, MSVC)
- Uses standard libraries:
  - `<iostream>`
  - `<string>`
  - `<ctime>`

**Resources**
- Requires moderate RAM for runtime object allocation
- Minimal disk space required

**User Experience**
- CLI-only interface, with future potential for GUI development

---

## Problem Analysis

This application addresses the need for academic-focused networking among students. It avoids the noise of traditional social platforms and fosters collaboration.

### Key Problems Addressed

1. **Focused Networking:** A space tailored for students
2. **Efficient Communication:** Simple and structured messaging
3. **Collaborative Groups:** Course-based study group system
4. **Undo Functionality:** Revert accidental actions

---

## Class Descriptions

### 1. `StudentProfile` Class

**Purpose:** Manage student data and interactions

**Attributes:**
- `string name`, `course`, `matric_no`
- `StudentProfile* next`, `prev`
- `MessageQueue inbox`
- `StudentProfile** friends`
- `int friendCount`, `friendCapacity`
- `FriendRequest* friendRequestsHead`

**Key Methods:**
- Constructor & Destructor
- `addFriend`, `removeFriend`
- `sendFriendRequest`, `viewFriendRequests`
- `listFriends`

---

### 2. `Message` Class

**Purpose:** Represents individual messages

**Attributes:**
- `string content`, `timestamp`
- `Message* next`

**Key Methods:**
- Constructor & Destructor
- `getContent`, `getTimestamp`
- `setNext`, `getNext`

---

### 3. `ActionStack` Class

**Purpose:** Implements undo functionality using Stack

**Attributes:**
- `Node* topNode`

**Key Methods:**
- Constructor & Destructor
- `push`, `pop`
- `isEmpty`

---

### 4. `MultiStudyGroup` Class

**Purpose:** Manage course-based study groups (Circular Linked List)

**Attributes:**
- `CourseGroup* head`

**Key Methods:**
- Constructor & Destructor
- `addMember`, `removeMember`
- `listGroupMembers`, `displayGroupMembersOneByOne`

---

### 5. `UndoableAction` Class

**Purpose:** Encapsulates actions that can be undone

**Attributes:**
- `ActionType actionType`
- `StudentProfile* profile1`, `profile2`

**Key Methods:**
- Constructor & Destructor
- `getActionType`, `getProfile1`, `getProfile2`
- `clearProfilePointers`

---

## Template Classes

### 6. `ProfileList` Class

**Purpose:** Manages student profiles (Doubly Linked List)

**Attributes:**
- `T* head`, `tail`

**Key Methods:**
- `addProfile`, `findProfile`, `removeProfile`
- `listProfilesForward`, `listProfilesBackward`
- `displayProfilesOneByOne`

---

### 7. `MessageQueue` Class

**Purpose:** Manages message queue for each student (FIFO)

**Attributes:**
- `Message* front`, `rear`

**Key Methods:**
- `enqueue`
- `getFront`
- `displayAll`
- `removeLastMessageFromSender`

---

## Exception Handling Example

```cpp
try {
    p  =  new StudentProfile(name, course, matric_no);
    profileList.addProfile(p);
    multiStudyGroup.addMember(p);
    actionStack.push(new UndoableAction(ActionType::CREATE_PROFILE, p));
    cout << "Profile created.\n";
} catch (...) {
    cout << "Error creating profile.\n";
    if (p) delete p;
}
