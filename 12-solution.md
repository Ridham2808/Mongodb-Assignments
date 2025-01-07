#### **Task 1: Add more students to the `students` collection**  
- Add at least 5 new students to the `students` collection with unique names, roll numbers, and course enrollments.
  
  ```js
  db.students.insertMany([
  {
    name: "Garvit",
    rollNumber: "CSE101",
    department: "CSE",
    year: 2,
    coursesEnrolled: ["C++10", "MATHS201", "Che102"],
  },
  {
    name: "Prem",
    rollNumber: "CSE102",
    department: "IT",
    year: 1,
    coursesEnrolled: ["C++10", "CHE102"],
  },
  {
    name: "Dhruv",
    rollNumber: "CSE103",
    department: "CSE",
    year: 3,
    coursesEnrolled: ["FIGMA100", "UI122"],
  },
  {
    name: "Aarya",
    rollNumber: "CSE104",
    department: "ECE",
    year: 2,
    coursesEnrolled: ["UI122", "MATHS201"],
  },
  {
    name: "Jatin",
    rollNumber: "CSE105",
    department: "ECE",
    year: 2,
    coursesEnrolled: ["FIGMA100", "C++10"],
  },
  ]);
  ```

#### **Task 2: Insert a new course into the `courses` collection**  
- Add a new course with the following details:  
  - Course Code: `CS202`  
  - Name: `Data Structures`  
  - Credits: 3  
  - Instructor: `Prof. Krishna`

  ```js
  db.courses.insertOne(
  {
    courseCode: "CS202",
    name: "Data Structures",
    credits: 3,
    instructor: "Prof. Krishna",
  })
  ```

#### **Task 3: Fetch a specific student's record by roll number**  
- Use `find()` to fetch a student's information using their roll number (`CS1002`).

  ```js
  db.students.find({ rollNumber: "CS1002" });
  ```

#### **Task 4: Query all students who are enrolled in a particular course**  
- Retrieve all students who are enrolled in "MATH101".

  ```js
  db.students.find({ coursesEnrolled: "MATH101" });
  ```

#### **Task 5: Update a student's courses**  
- Update the student with roll number `CS1001` to enroll in an additional course "CS202".

  ```js
  db.students.updateOne(
  { rollNumber: "CS1001" },
  { $push: { coursesEnrolled: "CS202" } }
  );
  ```

#### **Task 6: Remove a course from a student's courses list**  
- Remove the course `MATH101` from the student `Mahir`'s list of enrolled courses.

  ```js
  db.students.updateOne(
  { name: "Mahir" },
  { $pull: { coursesEnrolled: "MATH101" } }
  );
  ```

#### **Task 7: Find all courses with 3 credits**  
- Query the `courses` collection to find all courses where the `credits` field equals 3.

  ```js
  db.courses.find({ credits: 3 });
  ```

#### **Task 8: Find students who have enrolled in more than 2 courses**  
- Use `$size` operator to query students who are enrolled in more than 2 courses.

  ```js
  db.students.find({
  $expr: { $gt: [{ $size: "$coursesEnrolled" }, 2] }
  });
  ```

#### **Task 9: Use the `$in` operator to find students enrolled in multiple courses**  
- Use the `$in` operator to find students who are enrolled in either `CS101` or `MATH202`.

  ```js
  db.students.find({
  coursesEnrolled: { $in: ["CS101", "MATH202"] }
  });
  ```

#### **Task 10: Fetch all students from a specific department (e.g., CSE)**  
- Use a query to find all students in the `CSE` department.

  ```js
  db.students.find({ department: "CSE" });
  ```

#### **Task 11: Query students who are in their 3rd year**  
- Retrieve students who are in the `3rd` year using the `year` field.

  ```js
  db.students.find({ year: 3 });
  ```

#### **Task 12: Query students using a range for their year**  
- Find all students who are in `2nd` or `3rd` year by using the `$gte` operator.

  ```js
  db.students.find({ year: { $gte: 2, $lte: 3 } });
  ```

#### **Task 13: Count the total number of students in each department**  
- Use the `$group` stage of aggregation to group students by department and count them.

  ```js
  db.students.aggregate([
  {
    $group: {
      _id: "$department",
      totalStudents: { $sum: 1 }
    }
  }
  ]);
  ```

#### **Task 14: Group courses by credits**  
- Group courses by their credit value and count how many courses there are for each credit value.

  ```js
  db.courses.aggregate([
  {
    $group: {
      _id: "$credits",
      totalCourses: { $sum: 1 }
    }
  }
  ]);
  ```

#### **Task 15: Find the highest credit course**  
- Query for the course with the highest number of credits using the `$sort` operator.

  ```js
  db.courses.find().sort({ credits: -1 }).limit(1);
  ```

#### **Task 16: Use the `$and` operator for filtering students**  
- Find all students who belong to the `CSE` department and are enrolled in more than 2 courses.

  ```js
  db.students.find({
  $and: [
    { department: "CSE" },
    { "coursesEnrolled.2": { $exists: true } }
  ]
  });
  ```

#### **Task 17: Add a new field to all documents in the `students` collection**  
- Add a new field `activeStatus` and set it to `true` for all students.

  ```js
  db.students.updateMany(
  {},
  { $set: { activeStatus: true } }
  );
  ```

#### **Task 18: Use `$rename` to rename a field**  
- Rename the `coursesEnrolled` field in the `students` collection to `enrolledCourses`.

  ```js
  db.students.updateMany(
  {},
  { $rename: { "coursesEnrolled": "enrolledCourses" } }
  );
  ```

#### **Task 19: Set default values for new fields in all student documents**  
- Add a field `graduationYear` with a default value for all students.

  ```js
  db.students.updateMany(
  {},
  { $set: { graduationYear: 2025 } }
  );
  ```

#### **Task 20: Use the `$push` operator to add a new course to a student’s course list**  
- Add the course "CS303" to `Mahir`’s `coursesEnrolled` list.

  ```js
  db.students.updateOne(
  { name: "Mahir" },
  { $push: { coursesEnrolled: "CS303" } }
  );
  ```

#### **Task 21: Use `$pull` to remove a course from a student's courses list**  
- Remove the course `CS101` from `Jenil`’s list.

  ```js
  db.students.updateOne(
  { name: "Jenil" },
  { $pull: { coursesEnrolled: "CS101" } }
  );
  ```

#### **Task 22: Remove a student from the `students` collection**  
- Delete the student record with roll number `CS1004`.

  ```js
  db.students.deleteOne({ rollNumber: "CS1004" });
  ```

#### **Task 23: Find students who are enrolled in both `CS101` and `MATH202`**  
- Use `$all` operator to find students who are enrolled in both courses.

  ```js
  db.students.find({ enrolledCourses: { $all: ["UI122","FIGMA100"] } })
  ```

#### **Task 24: Use `$regex` to search for students whose name starts with "A"**  
- Use regular expressions to search for students whose names begin with the letter "A".

  ```js
  db.students.find({ name: { $regex: "^A" } });
  ```

#### **Task 25: Use `$exists` to find students with enrolled courses**  
- Query students who have an entry in the `coursesEnrolled` array.

  ```js
  db.students.find({ enrolledCourses: { $exists: true } });
  ```

#### **Task 26: Add a field to store students' grades for each course**  
- Add a new field `grades` to the `students` collection and store an array of grades for each course.

  ```js
  db.students.updateMany(
  {},
  { $set: { grades: [] } }
  );
  ```

#### **Task 27: Use `$elemMatch` to query students enrolled in specific courses**  
- Find students enrolled in `CS101` and have the grade `A`.

  ```js
  db.students.find({
  rollNumber: "CS1001",
  grades: { $elemMatch: { grade: "A" } }
  });
  ```