---
layout: post
title: "How to edit gitignore file for Xcode project"
date: 2015-06-11 10:00:49 +0800
comments: true
categories: 
---

A gitignore file specifies intentionallly untracked files that Git should ignore. Each line in a gitignore file sepecifies a pattern. We can see the detail as follows:    
<!--more-->  


##PATTERN FORMAT
* A blank line matches no files, so it can serve as a separator for readability.  

* A line starting with # serves as a comment. Put a backslash ("\\") in front of the first hash for patterns that begin with a hash.  

* Trailing spaces are ignored unless they are quoted with backslash ("\\").  

* An optional prefix "!" which negates the pattern; any matching file excluded by a previous pattern will become included again. It is not possible to re-include a file if a parent directory of that file is excluded. Git doesn’t list excluded directories for performance reasons, so any patterns on contained files have no effect, no matter where they are defined. Put a backslash ("\\") in front of the first "!" for patterns that begin with a literal "!", for example, "\!important!.txt".  

* If the pattern ends with a slash, it is removed for the purpose of the following description, but it would only find a match with a directory. In other words, foo/ will match a directory foo and paths underneath it, but will not match a regular file or a symbolic link foo (this is consistent with the way how pathspec works in general in Git).      

* If the pattern does not contain a slash /, Git treats it as a shell glob pattern and checks for a match against the pathname relative to the location of the .gitignore file (relative to the toplevel of the work tree if not from a .gitignore file).  

Two consecutive asterisks ("**") in patterns matched against full pathname may have special meaning:  

* A leading "\*\*" followed by a slash means match in all directories. For example, "\*\*/foo" matches file or directory "foo" anywhere, the same as pattern "foo". "\*\*/foo/bar" matches file or directory "bar" anywhere that is directly under directory "foo".  

* A trailing "/\*\*" matches everything inside. For example, "abc/\*\*" matches all files inside directory "abc", relative to the location of the .gitignore file, with infinite depth.  

* A slash followed by two consecutive asterisks then a slash matches zero or more directories. For example, "a/\*\*/b" matches "a/b", "a/x/b", "a/x/y/b" and so on.  

* Other consecutive asterisks are considered invalid.
  
##Notice  

Patterns read from a .gitignore file in the same directory as the path, or in any parent directory, with patterns in the higher level files (up to the toplevel of the work tree) being overridden by those in lower level files down to the directory containing the file.   

##gitignore file for xcode
```  

## Build generated
# slash on the end, so we only remove the FOLDER, not any files that were badly named "DerivedData"
build/
DerivedData/

#####
# Xcode private settings (window sizes, bookmarks, breakpoints, custom executables, smart groups)
#
# This is complicated:
#
# SOMETIMES you need to put this file in version control.
# Apple designed it poorly - if you use "custom executables", they are
#  saved in this file.
# 99% of projects do NOT use those, so they do NOT want to version control this file.
#  ..but if you're in the 1%, comment out the line "*.pbxuser"

# .pbxuser: http://lists.apple.com/archives/xcode-users/2004/Jan/msg00193.html

*.pbxuser

# .mode1v3: http://lists.apple.com/archives/xcode-users/2007/Oct/msg00465.html

*.mode1v3

# .mode2v3: http://lists.apple.com/archives/xcode-users/2007/Oct/msg00465.html

*.mode2v3

# .perspectivev3: http://stackoverflow.com/questions/5223297/xcode-projects-what-is-a-perspectivev3-file

*.perspectivev3

# also, whitelist the default ones, some projects need to use these
!default.pbxuser
!default.mode1v3
!default.mode2v3
!default.perspectivev3


# OPTION 1: ---------------------------------
#     throw away ALL personal settings (including custom schemes!
#     - unless they are "shared")
# As per build/ and DerivedData/, this ought to have a trailing slash
#
# NB: this is exclusive with OPTION 2 below
xcuserdata/

# OPTION 2: ---------------------------------
#     get rid of ALL personal settings, but KEEP SOME OF THEM
#     - NB: you must manually uncomment the bits you want to keep
#
# NB: this *requires* git v1.8.2 or above; you may need to upgrade to latest OS X,
#    or manually install git over the top of the OS X version
# NB: this is exclusive with OPTION 1 above
#
#xcuserdata/**/*

#     (requires option 2 above): Personal Schemes
#
#!xcuserdata/**/xcschemes/*

####
# Xcode 4 - semi-personal settings
#
# Apple Shared data that Apple put in the wrong folder
# c.f. http://stackoverflow.com/a/19260712/153422
#     FROM ANSWER: Apple says "don't ignore it"
#     FROM COMMENTS: Apple is wrong; Apple code is too buggy to trust; there are no known negative side-effects to ignoring Apple's unofficial advice and instead doing the thing that actively fixes bugs in Xcode
# Up to you, but ... current advice: ignore it.
*.xccheckout
*.moved-aside
*.xcuserstate

####
# XCode 4 workspaces - more detailed
#
# Workspaces are important! They are a core feature of Xcode - don't exclude them :)
#
# Workspace layout is quite spammy. For reference:
#
# /(root)/
#   /(project-name).xcodeproj/
#     project.pbxproj
#     /project.xcworkspace/
#       contents.xcworkspacedata
#       /xcuserdata/
#         /(your name)/xcuserdatad/
#           UserInterfaceState.xcuserstate
#     /xcshareddata/
#       /xcschemes/
#         (shared scheme name).xcscheme
#     /xcuserdata/
#       /(your name)/xcuserdatad/
#         (private scheme).xcscheme
#         xcschememanagement.plist
#
#

## Obj-C/Swift specific
*.hmap
*.ipa

####
# OPTIONAL: Some well-known tools that people use side-by-side with Xcode / iOS development
#
# NB: I'd rather not include these here, but gitignore's design is weak and doesn't allow
#     modular gitignore: you have to put EVERYTHING in one file.
#
# COCOAPODS:
#
# c.f. http://guides.cocoapods.org/using/using-cocoapods.html#what-is-a-podfilelock
# c.f. http://guides.cocoapods.org/using/using-cocoapods.html#should-i-ignore-the-pods-directory-in-source-control
#
#!Podfile.lock
#Pods
#
# RUBY:
#
# c.f. http://yehudakatz.com/2010/12/16/clarifying-the-roles-of-the-gemspec-and-gemfile/
#
#!Gemfile.lock
#
# IDEA:
#
#.idea
#
# TEXTMATE:
#
# -- UNVERIFIED: c.f. http://stackoverflow.com/a/50283/153422
#
#tm_build_errors

####
# UNKNOWN: recommended by others, but I can't discover what these files are
#
# Community suggestions (unverified, no evidence available - DISABLED by default)
#
# 1. Xcode 5 - VCS file
#
# "The data in this file not represent state of your project.
# If you'll leave this file in git - you will have merge conflicts during 
# pull your cahnges to other's repo"
#
#*.xccheckout


```


##Reference  

1. http://git-scm.com/docs/gitignore   
2. http://stackoverflow.com/questions/49478/git-ignore-file-for-xcode-projects  

