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
