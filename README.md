# knn
knn

🔑 צעדים לפתרון תרגיל KNN
1️⃣ להבין את הבעיה

מה רוצים לסווג/לחזות?
(למשל: פרי חדש → האם תפוח/תפוז/בננה, או לקוח חדש → האם יחזיר הלוואה).

מהן התכונות (features)?
(גיל, הכנסה, ותק; או צבע, משקל, גודל).

מה היעד (label)?
(כן/לא, סוג פרי, קטגוריה).

2️⃣ להכין את הדאטה

לארגן את הנתונים ל־X (מאפיינים) ו־y (תוויות).

לבדוק אם יש סקאלות שונות בין התכונות.
אם כן → חייבים Scaling (לרוב Min-Max או Standardization).

3️⃣ נרמול / Scaling

להשתמש ב־MinMaxScaler או StandardScaler.

חשוב: ל־fit רק על דאטת האימון, ואז transform גם לאימון וגם לטסט.
(כדי לא לדלוף מידע עתידי).

4️⃣ בחירת K

להתחיל מ־k קטן (3, 5).

אם צריך, להשתמש ב־GridSearchCV כדי למצוא את ה־k האופטימלי.

לשים לב: k זוגי עלול לגרום לשוויון → לכן לרוב מתחילים מ־k אי־זוגי.

5️⃣ בחירת metric

Euclidean (מרחק פיתגורס) – ברירת מחדל.

Manhattan (סכום הפרשים) – לפעמים יציב יותר ברעש.

נבדוק מה עובד טוב יותר עם GridSearchCV.

6️⃣ אימון המודל
model = KNeighborsClassifier(n_neighbors=k, metric="euclidean")
model.fit(X_train_scaled, y_train)

7️⃣ חיזוי
prediction = model.predict(X_test_scaled)
probabilities = model.predict_proba(X_test_scaled)


לקבל סיווג (כן/לא / תפוח/בננה/תפוז).

להציג הסתברויות למחלקות.

8️⃣ הערכת המודל

לחשב דיוק (accuracy) או מדדים אחרים (precision, recall, f1).

לוודא שהמודל לא overfitting (k קטן מדי) או underfitting (k גדול מדי).

9️⃣ חיזוי עבור דוגמא חדשה

לקחת את ערכי הלקוח/הפרי החדש.

לעשות transform עם אותו scaler.

להכניס למודל ולחזות.

⚡ שאלות שכדאי לשאול את עצמי בתרגיל KNN

האם יש תכונות עם סולמות שונים? אם כן → עשיתי scaling?

איזה מרחק מתאים? euclidean או manhattan?

איזה k ייתן את האיזון הכי טוב?

כמה מחלקות יש? האם מאוזנות?

האם אני בודק את המודל עם train/test או CV ולא רק על אותו דאטה?





הנה דיאגרמת זרימה (Flowchart) שמסכמת איך ניגשים לתרגיל KNN – שלב אחר שלב 📊

קודם להבין את הבעיה והנתונים

להכין X ו־y

לבצע נרמול / Scaling

לבחור k ו־Metric מתאים

לאמן את המודל

לבדוק ביצועים (CV/Test)

בסוף לחזות נקודה חדשה



📝 דוגמה מוקטנת (במבנה אחיד)

# 1. דאטה
X = [[22,60,1], [25,75,2], [30,80,3], ...]
y = ["לא","לא","כן",...]

# 2. נרמול
scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)

# 3. מודל
knn = KNeighborsClassifier(n_neighbors=3, metric="euclidean")
knn.fit(X_scaled, y)

# 4. חיזוי ללקוח חדש
new_client = [[27,95,3]]
new_client_scaled = scaler.transform(new_client)
print(knn.predict(new_client_scaled))


🔔 לסיכום:
כשמקבלים תרגיל KNN – קודם מסדרים את הדאטה, עושים נרמול, מגדירים k ומרחק, מאמנים את המודל, בודקים דיוק עם CV, ואז מחזים על נקודות חדשות.
