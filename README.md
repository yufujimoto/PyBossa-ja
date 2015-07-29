# How to apply Japanese translation file to PyBossa

1. Create a symlink to the translation directory to enable translation file. 

        cd ~/pybossa/pybossa && ln -s themes/defaul/translations

2. Initialyze the translation directory under "~/pybossa/pybossa/translations/".  
    
        pybabel init -i messages.pot -d translations -l ja

3. Open "~/pybossa/pybossa/forms/forms.py" and add a new language settings around line 305.
    
        if locale == 'ja':
            lang = gettext("Japanese")

4. Open /pybossa/default_settings.py and a new language settings in LOCALES as below:
    
        LOCALES = ['en', 'es', 'it', 'fr', '**ja**']


5. Rewrite the default user settings in /pybossa/model/user.py as bebelow:
    
        locale = Column(Unicode(length=254), default=u'ja', nullable=False)

6. Replace **messages.pot** file located in "~/pybossa/pybossa/translations/".

7. Restart PyBossa.
    
        cd ~/pybossa/pybossa  
        pybabel extract . -F babel.cfg -k lazy_gettext -o translations/messages.pot
        pybabel update -i translations/messages.pot -d translations
        pybabel compile -d translations
        python ../run.py

