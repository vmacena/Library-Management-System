# Object-oriented programming challenge

Change the application so that the number of books currently on loan to a user is also obtained from the database, in order to solve the existing bug in the system.


![update](https://github.com/vmacena/Library-Management-System/assets/83997291/cc2f740c-aeb1-424e-beea-d4dd833f605f)

public int getBorrowedBooksCount(User user) {
        String userId = user.getInstitutionalId();
        if (userId == null) {
            throw new IllegalArgumentException("User ID must not be null.");
        }
    
        String sql = "SELECT COUNT(*) FROM BookTransaction WHERE user = ?";
    
        try (PreparedStatement stmt = ConnectionFactory.createPreparedStatement(sql)) {
            stmt.setString(1, userId);
            ResultSet resultSet = stmt.executeQuery();
            if (resultSet.next()) {
                return resultSet.getInt(1);
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    
        return 0;
    }
}
