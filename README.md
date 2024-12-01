# odoo17_learning
odoo17_day_wise_learning

#Day_1
### Step-by-Step Notes for Odoo 17 Development Practice

###1. **Introduction to Odoo 17 Development**  
   - If you have experience with Odoo 15 or 16, you can directly work with Odoo 17.  
   - This guide is aimed at absolute beginners for setting up and developing in Odoo 17.

###2. **Setting Up the Development Environment**  
   - Download and install **PyCharm Community Edition** (or Professional) for development.
   - Use **Odoo 17** with PyCharm IDE for development.
   - You can follow the setup tutorial for Odoo 15/16 and apply the same steps for Odoo 17.
   
###3. **Setting Up Odoo 17**  
   - Clone the Odoo 17 Enterprise and Community source codes into a directory named `git` (e.g., `git/enterprise` and `git/community`).
   - Odoo development for both **Enterprise** and **Community** editions is the same, with no major technical differences.
   
###4. **Configure Odoo in PyCharm**  
   - Inside the **PyCharm IDE**, you need to set the Odoo configuration file for your project.
   - The configuration should include the `addons_path` and admin credentials.
   
###5. **Creating the Odoo Database**  
   - On running Odoo, it will ask to create a new database. 
   - Name the database (e.g., `odoo17_development`), set an admin email and password, and load demo data.
   
###6. **Setting Up Custom Addons Path**  
   - Inside the **Odoo configuration file**, create a directory for **custom addons** and set it in the `addons_path`.
   - Ensure the Odoo user has the necessary permissions to access the custom directory.

###7. **Creating Your First Odoo Module**  
   - Create a new directory under `custom_addons` (e.g., `om_hospital`).
   - Inside this directory, create two important files:  
     - **`__init__.py`**  
     - **`__manifest__.py`**
     
###8. **Writing the `__manifest__.py` File**  
   - The `manifest.py` contains metadata about the module, such as the module's name, version, author, and license.
   - Example of `__manifest__.py` content:
     ```python
     {
         'name': 'Hospital Management System',
         'version': '17.0.1',
         'author': 'Your Name',
         'license': 'LGPL-3',
         'category': 'Healthcare',
     }
     ```
   - Add more details later, such as dependencies and application views.

###9. **Activating Developer Mode**  
   - In Odoo, go to **Settings > Activate Developer Mode** to see developer features, like accessing the Apps menu and enabling new modules.

###10. **Updating the App List**  
    - After adding a new module, click **Update App List** in the Odoo UI to refresh the available apps.
    - Search for the new module (e.g., `Hospital Management System`) and install it.

###11. **Creating Models in Odoo**  
    - Create a new folder called **models** inside the module directory (e.g., `om_hospital/models`).
    - Create an **`__init__.py`** file inside the models folder and import necessary Odoo modules.
    - Create a Python file (e.g., `patient.py`) where you define your model class to store patient information.

###12. **Example of a Simple Model for Patients**  
    - In **`patient.py`**, define a new model called `HospitalPatient` using Odoo's ORM:
      ```python
      from odoo import models, fields

      class HospitalPatient(models.Model):
          _name = 'hospital.patient'
          _description = 'Hospital Patient'

          name = fields.Char('Name', required=True)
          age = fields.Integer('Age')
          gender = fields.Selection([('male', 'Male'), ('female', 'Female')], 'Gender')
          diagnosis = fields.Text('Diagnosis')
      ```
    - This model will create a corresponding table in the PostgreSQL database.

###13. **Testing the Module**  
    - After creating the module and models, restart the Odoo service and update the app list again.
    - You should see your new module in the apps menu, and you can install it.
    - Check the backend of the module for features like adding patient records.

###14. **Version Control and Git**  
    - Use Git to manage your Odoo project source code. Ensure the repository includes both **custom addons** and **Odoo configuration files**.
    - Commit and push changes regularly to keep your project version-controlled.

###15. **Additional Customizations**  
    - Continue to develop your module by adding views, forms, and reports.
    - Add icons and further metadata to the manifest file as needed.
    - Expand your module's functionality by linking it with other Odoo apps like Sales or Inventory.

### 16. **Set up the Patient Model (hospital_patient.py)**:
   - You imported `API` fields and `models` from Odoo.
   - Created a class `HospitalPatient`, inheriting from `models.Model`.
   - Defined the model with a description, e.g., "Patient Master."
   - The model definition creates a table in the PostgreSQL database automatically upon upgrading the module.

### 17. **Add Fields to the Patient Model**:
   - Added fields such as `name` (character field), `date_of_birth` (date field), and `gender` (selection field with values "Male" and "Female").
   - After modifying the Python code, you restarted the service and upgraded the module to reflect the new fields in the database.

### 18. **Create Views Directory**:
   - Inside the Odoo module, you created a directory called `views` to hold view-related files (such as menus and actions).

### 19. **Create the Menu (menu.xml)**:
   - Created a `menu.xml` file in the `views` directory, where you defined the main menu `Hospital Management System (HMS)` using the `<menuitem>` tag.
   - Imported this XML file into the `__manifest__.py` file.

### 20. **Add Submenus and Parent-Child Relationships**:
   - You added a submenu for the front desk under the main HMS menu and linked it as a child menu using the `parent` key.
   - You also created a submenu for "Patient" under the front desk, making it part of the existing menu structure.

### 21. **Define an Action for the Patient Menu**:
   - Created a new action `act_window` to link the "Patient" menu to a view displaying patient records.
   - Added a view mode with `tree` and `form` views to manage patient data.

### 22. **Fix the Order of XML Files in `__manifest__.py`**:
   - You fixed an issue where the action was being loaded after the menu, causing errors. By placing the action before the menu definition in the `__manifest__.py` file, the system could process the action first before the menu.

### 23. **Security Configuration for Patient Model**:
   - Created a `security` folder and defined the access control rules in `ir.model.access.csv`, setting permissions for the "HospitalPatient" model.
   - Added access rights for read, write, create, and unlink actions for the "base.group_user" group (internal users).
   - Imported the security file into the `__manifest__.py` file to ensure it's loaded correctly.

### 24. **Superuser Access for Testing**:
   - To bypass security restrictions, you activated superuser mode to test the creation of a new patient record and confirm that the menu and actions were working properly.

### 25. **Final Testing and Debugging**:
   - You logged out of the superuser mode and tested the patient menu, confirming that the action and the related views were working as expected.
   - Verified the patient creation functionality, ensuring the data could be saved correctly.
---

#Day_2

### 26. Odoo 17: Working with Views in Hospital Management System (HMS)
- **Creating and Managing Records**: When you create a new patient, fields such as name, date of birth, and gender are recorded, and the record's ID is displayed in the URL.
- **Metadata in Debug Mode**: By enabling the debug mode, you can access metadata like the create user, create date, last modification user, and modification date from the "View Metadata" option in the debugger.

### 27. Auto-Generated Views
- If no views are defined for a model, Odoo automatically generates dynamic views based on the model's fields.
- This dynamic view can be edited by clicking "Edit View Form" in the debugger, but it's better to define your own views for better control.

### 28. Defining Tree View in Odoo
- **Creating Tree View**: To define a tree view for the `hospital.patient` model, use the `<tree>` tag in XML. Define the model and link the fields to be displayed in the view.
- **Upgrading the Module**: After defining the tree view, upgrade the module to see the new view in the UI.

### 29. Defining Form View in Odoo
- **Creating Form View**: Similar to the tree view, you can define a form view using the `<form>` tag. Ensure to use `<group>` tags to organize fields and `<sheet>` tag for layout control.
- **Grouping Fields**: To organize fields into multiple columns, use nested `<group>` tags inside the `<form>` tag. This can help in visually dividing the fields into sections.
  
### 30. Using Optional Fields in Views
- **Optional Show/Hide**: To manage field visibility, you can use the `optional_show` and `optional_hide` attributes. By default, hidden fields are not visible but can be toggled by the user.

### 31. Odoo Chatter for Tracking Changes
- **Chatter for Change Tracking**: In Odoo, the chatter section tracks changes made to a record (e.g., name changes, phone number updates).
- **Implementing Chatter in Custom Models**: To add chatter functionality, inherit the `mail.thread` class in your model. This allows tracking of changes and updates in the record.

### 32. Adding Dependencies in Odoo Modules
- **Inheriting Mail.Thread**: When inheriting `mail.thread` to enable chatter, you need to add the `mail` module as a dependency in the manifest file (`depends`).
- **Upgrading the Module**: After adding the inheritance and dependencies, upgrade the module to apply changes.
Here are the notes for your Odoo practice (starting from serial number 33):

---

**33. Inheriting `mail.thread` and Adding Chatter**
- The `mail.thread` module has been added as a dependency, which adds several new fields to the model (like `message_follower_ids`, `message_ids`).
- To include the chatter in the view, copy the chatter section from the Odoo source code.
- Add the chatter code within the form view, after the `sheet` tag.
- After a restart, the "Send Message" and "Log Note" options appear in the form view.

---

**34. Tracking Field Changes**
- To track changes in a field, set `tracking=True` in the field definition.
- After adding the tracking attribute, restart the system and upgrade the module to see changes reflected in the "Log Note" and "Send Message" sections.
- Ensure tracking is added to fields like `name`, `date_of_birth`, and `gender` to log updates.

---

**35. Adding Multiple Views for a Model**
- You can define multiple views (e.g., read-only views) for the same model.
- When creating a new view, ensure a unique `ID` is used for each action.
- The system will throw an error if the action is not defined; ensure the action is correctly linked in the XML.
  
---

**36. Restricting Edit Permissions in Read-Only Views**
- To create a read-only version of the view, specify `create="0"` and `edit="0"` in the XML.
- This restricts the user from creating or editing records in the view.

---

**37. Sequence and Priority in Views**
- When defining multiple views for the same model, use the `sequence` attribute to determine which view is shown by default. Odoo will select the view with the lowest sequence number if no specific view is linked.
- Alternatively, use `priority` to control the order of views if sequence values are the same.

---

**38. Using `view_ids` in Actions**
- Use the `view_ids` attribute in the action to specify which views should be shown for the action.
- This allows you to link different tree and form views with the action.
- To hide the "New" button in a view, set `create="0"` in the tree and form view.

---

**39. Module Upgrade and Troubleshooting**
- When making changes to views or adding new actions, always remember to upgrade the module to apply those changes.
- If an error occurs, check the action definitions and ensure that any new views or menu items are linked correctly.

---
