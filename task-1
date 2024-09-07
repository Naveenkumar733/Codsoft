import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

data = pd.read_csv('Titanic-Dataset.csv')
data['Age'].fillna(data['Age'].median(), inplace=True)
data['Fare'].fillna(data['Fare'].median(), inplace=True)
data['Cabin'].fillna('Unknown', inplace=True)

data = data[['Survived', 'Pclass', 'Sex', 'Age', 'Fare', 'Cabin']]

label_encoder_sex = LabelEncoder() # Create a new LabelEncoder for 'Sex'
data['Sex'] = label_encoder_sex.fit_transform(data['Sex'])

label_encoder_cabin = LabelEncoder() # Create a new LabelEncoder for 'Cabin'
data['Cabin'] = label_encoder_cabin.fit_transform(data['Cabin'])

X = data.drop('Survived', axis=1)
y = data['Survived']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

accuracy = accuracy_score(y_test, y_pred)
print(f'Accuracy: {accuracy:.2f}')

new_data = pd.DataFrame({
    'Pclass': [2],
    'Sex': [label_encoder_sex.transform(['female'])], # Use the correct LabelEncoder for 'Sex'
    'Age': [30],
    'Fare': [10],
    'Cabin': [label_encoder_cabin.transform(['Unknown'])[0]] # Use the correct LabelEncoder for 'Cabin'
})
prediction = model.predict(new_data)
print(f'Survived: {"Yes" if prediction[0] else "No"}')
