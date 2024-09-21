Тесты для add_new_book:
    def test_add_new_book(self, collector):
        collector.add_new_book("Гарри Поттер")
        assert "Гарри Поттер" in collector.get_books_genre()

    def test_add_new_book_name_too_long(self, collector):
        long_name = "Книга с очень длинным названием, которое больше 40 символов"
        collector.add_new_book(long_name)
        assert long_name not in collector.get_books_genre()

    def test_add_new_book_does_not_add_if_already_exists(self, collector):
        collector.add_new_book("Гарри Поттер")
        collector.add_new_book("Гарри Поттер")
        assert len(collector.get_books_genre()) == 1

Тесты для set_book_genre:

    def test_set_book_genre(self, collector):
        collector.add_new_book("Гарри Поттер")
        collector.set_book_genre("Гарри Поттер", "Фантастика")
        assert collector.get_book_genre("Гарри Поттер") == "Фантастика"

    def test_get_books_with_specific_genre_no_books(self, collector):
        assert collector.get_books_with_specific_genre("Фантастика") == []

Тест для get_books_for_children:

    def test_get_books_for_children_only_age_restricted(self, collector):
        collector.add_new_book("Ужасный фильм")
        collector.set_book_genre("Ужасный фильм", "Ужасы")
        assert collector.get_books_for_children() == []

Тест для add_book_in_favorites:

    def test_add_book_in_favorites_invalid_book(self, collector):
        collector.add_book_in_favorites("Неизвестная книга")
        assert "Неизвестная книга" not in collector.get_list_of_favorites_books()

Тест для delete_book_from_favorites:

    def test_delete_book_from_favorites_not_in_favorites(self, collector):
        collector.add_new_book("Гарри Поттер")
        collector.delete_book_from_favorites("Гарри Поттер")
        assert "Гарри Поттер" not in collector.get_list_of_favorites_books()

Тест для get_list_of_favorites_books:

    def test_get_list_of_favorites_books(self, collector):
        collector.add_new_book("Гарри Поттер")
        collector.add_book_in_favorites("Гарри Поттер")
        assert collector.get_list_of_favorites_books() == ["Гарри Поттер"]