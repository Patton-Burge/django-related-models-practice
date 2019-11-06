Skip to content
Using Base Camp Coding Academy Mail with screen readers
in:sent

1 of 280
Quiz

Patton Burge <pburge@basecampcodingacademy.org>
Attachments
10:17 AM (4 hours ago)
to Nate

Quiz on Related DataBases

Patton Burge
Base Camp Coding Academy
Class of 2020
Attachments area

# 11/6/2019 - Related Models Quiz

## Defining Related Models

Define the following Models for a blog website: User, Post, Comment, Like, SocialLink

A User has: name, profile picture url, bio, hometown, date joined the website.

A Post has: an author, a banner image url, a title, content, publication date.

A Comment has: an author, a post, content, publication date.

A Like has: a user, and a post.

A SocialLink has: a user, a URL.

```python
class User(models.Model):
    name = models.TextField()
    profile_url = models.URLField()
    bio = models.TextField()
    hometown= models.TextField()
    date_joined = models.DateField()

class Post(models.Model):
    author = models.ForeignKey(User, on_delete=models.PROTECT)
    banner_url = models.URLField()
    title = models.TextField()
    content = models.TextField()
    publication_date = models.DateField()

class Comment(models.Model):
    author = models.ForeignKey(User, on_delete=models.PROTECT)
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    content = models.TextField()
    publication_date = models.DateField()

class Like(models.Model):
    user = models.ForeignKey(User, null=True, on_delete=models.SET_NULL)
    post = models.ForeignKey(Post, on_delete=models.CASCADE)

class SocialLink():
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    url = models.URLField()
```

## CRUD Operations

Given the following Model definitions, complete the following code snippets by adding the appropriate code
beneath each comment.

```python
class Team(models.Model):
    mascot = models.TextField()
    hometown = models.TextField(unique=True)

class Player(models.Model):
    name = models.TextField()
    team = models.ForeignKey(Team, null=True, on_delete=models.SET_NULL)
```

```python
# Create a team from "Water Valley" with "Blue Devil" as the mascot
team = Team.objects.create(mascot="Blue Devil", hometown="Water Valley")

# Get all the players who are not currently on a team
players_not_on_team = Player.objects.filter(team__isnull=True)

# Get all the players who play for the team whose hometown is "Starkville"
# players_in_starkville = Player.objects.filter(team__hometown__endswith="ville")
team = Team.objects.get(hometown="Starkville")
players = team.player_set.all()

# Create a new player named "Janie Sportslady" and put them on the team based
# out of Oxford
team = Team.objects.get(hometown="Oxford")
player = team.player_set.create(name="Janie Sportslady")

# Get all the players whose name starts with "B"
# For each of those players, print out their team's name
players = Player.objects.filter(name__startswith="B")
for player in players:
    print(player.team.name)

```

11_6_2019_related_models_quiz.md
Displaying 11_6_2019_related_models_quiz.md.
