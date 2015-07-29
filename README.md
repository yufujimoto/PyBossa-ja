# How to add Japanese menu to PyBossa 

1. Replace some files located in "~/pybossa/pybossa/themes/default/templates" with following files.

    + account/update.html
    + admin/dashboard.html
    + projects/delete.html
    + projects/index.html
    + projects/task_import_options.html
    + tasks_browse.html

2. Create a symlink to the translation directory to enable translation file. 

        cd ~/pybossa/pybossa && ln -s themes/defaul/translations

3. Initialyze the translation directory under "~/pybossa/pybossa/translations/".  
    
        pybabel init -i messages.pot -d translations -l ja

4. Open "~/pybossa/pybossa/forms/forms.py" and add a new language settings around line 305.
    
        if locale == 'ja':
            lang = gettext("Japanese")

5. Open /pybossa/default_settings.py and a new language settings in LOCALES as below:
    
        LOCALES = ['en', 'es', 'it', 'fr', 'ja']


6. Rewrite the default user settings in /pybossa/model/user.py as bebelow:
    
        locale = Column(Unicode(length=254), default=u'ja', nullable=False)

7. Replace **messages.pot** file located in "~/pybossa/pybossa/translations/".

    You can edit/modify the **messages.pot** file if you need.

8. Restart PyBossa.
    
        cd ~/pybossa/pybossa  
        pybabel extract . -F babel.cfg -k lazy_gettext -o translations/messages.pot
        pybabel update -i translations/messages.pot -d translations
        pybabel compile -d translations
        python ../run.py

